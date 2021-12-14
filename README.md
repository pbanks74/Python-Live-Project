# Tech-Academy-Projects
While studying at The Tech Academy, I completed several assignments and worked on multiple projects in order to build my skill set and proficiency in HTML, CSS, JavaScript, Python, Django, SQL, C# and the .NET framework. I was taught how to think like a programmer in order to find creative solutions while writing clean and precise commented code. Completing these assignments and projects taught me several programming skills and gives me the confidence that I can learn any language or framework fairly quickly.

## Python Live Project
After completing the Python course, I participated in a two week sprint. I was tasked with using Python within the Django framework to create a dynamic web application. I chose travel as my topic and I built a destinations website that allows a user to create, review, update and delete information about their favorite travel destinations. I used several functions in the views in order to retrieve data and display them on the applicable HTML template. Additionally, I connected an API and wrote a basic JSON response that allows the user to view the current temperature at that specific destination. Ideally, I would have utilized data scraping and API's to display the current flight price, which I plan to implement in the future. 

### Creating the Basic App
To start, I created a new application within the Django framework. I created base and home templates and then added function to the views in order for a homepage with a navbar to render. I then registered my URL's and linked my application to the main project home page.

### Creating the Model and Form
I created an object model class with a manager and defined it's attributes. 

    class destination(models.Model):
        TripName = models.CharField(max_length=30, default="", blank=False, null=False)
        City = models.CharField(max_length=20, default="", blank=False, null=False)
        State = models.CharField(max_length=20, choices=StateChoices, blank=True)
        Country = models.CharField(max_length=20, default="", blank=True, null=False)
        Notes = models.TextField(max_length=300, default="Notes", blank=True)

        # assigns a manager
        destination = models.Manager()

I then created a model form that includes any inputs the user needs to make. 

    from django.forms import ModelForm
    from .models import destination

    class DestinationForm(ModelForm):
        class Meta:
            model = destination
            fields = '__all__'
            
            
Additionally, I made a template page for the form and then created a views function that renders all trips in the database. Lastly, I added it to my urls file.

    <div>
        <table style="width:100%">
            <tr>
                <th>Trip Name</th>
                <th>City</th>
                <th>State</th>
                <th>Country</th>
                <th>Notes</th>
            </tr>
            <tr>
                <td>{{ details.TripName }}</td>
                <td>{{ details.City }}</td>
                <td>{{ details.State }}</td>
                <td>{{ details.Country }}</td>
                <td>{{ details.Notes }}</td>

            </tr>
        </table>
    </div>
    
    # function renders all trips in database
    def destinations(request):
        trips = destination.destination.all()
        content = {'trips': trips}
        return render(request, 'TravelDestinations/TravelDestinations_destinations.html', content)

    
    
I created the following function that displays all of the details of a specific trip to a details html page.

    # function displays the details of a specific trip
    def trip_details(request, id):
        details = destination.destination.get(id=id)
        content = {'details': details}
        return render(request, 'TravelDestinations/TravelDestinations_details.html', content)
        
### CRUD functionality

    #function saves the users new destination details to the database.
    
    def TravelDestinations_add(request):
       form = DestinationForm(data=request.POST or None)
       if request.method == 'POST':
           if form.is_valid():
               form.save()
               return redirect('TravelDestinations_add.html')
       content = {'form': form}
       return render(request, 'TravelDestinations/TravelDestinations_add.html', content)
    
    # function allows the user to edit trip details
    
    def trip_edit(request, id):
        item_details = get_object_or_404(destination, id=id)
        form = DestinationForm(request.POST or None, instance=item_details)
        if form.is_valid():
            form.save()
            return redirect('TravelDestinations_destinations.html')
        content = {'form': form}
        return render(request, 'TravelDestinations/TravelDestinations_edit.html', content)
        
    # function enables user to delete trips from database
    
    def trip_delete(request, id):
        data = get_object_or_404(destination, id=id)
        if request.method == 'POST':
            data.delete()
            return redirect('TravelDestinations_destinations.html')
        delete = {'data': data}
        return render(request, 'TravelDestinations/TravelDestinations_delete.html', delete)


### Connect to API
I created a new API template and rendered it with a function. I then researched API documentation in order to connect the API and write a basic JSON response that displays temperature in Fahreheit for a specific destination.

    def destination_weather(request):
    api = 'https://api.openweathermap.org/data/2.5/weather?q='
    city = 'Portland'
    apiKey = '&appid=080528254af16dbd0c82d7c43b425e9f'
    units = '&units=imperial'
    url = api + city + apiKey + units
    response = requests.get(url)
    weather = response.json()
    content = {'weather': weather}
    return render(request, 'TravelDestinations/TravelDestinations_weather.html', content)


    # basic function to get API response. 'units=imperial' displays results in Fahrenheit for portland
    '''
    def destination_weather(request):
        response = requests.get('https://api.openweathermap.org/data/2.5/weather?q=portland&units=imperial&appid=080528254af16dbd0c82d7c43b425e9f')
        print(response.status_code)
        print(response.json())
        weather = response.json()
        content = {'weather': weather}
        return render(request, 'TravelDestinations/TravelDestinations_weather.html', content)
    '''
    
###Conclusion
The Python live project provided me with my first opportunity to utilize project methodologies and gain a detailed understanding of version control. I worked with other students within an Agile framework environment on the Microsoft Azure DevOps platform. I was able to make commits, merges and push/pulls in real time while being aware of how to minimize merge conflicts. I participated in daily standup meetings to discuss progress and roadblocks as well as a retrospective meeting upon completion. I look forward to utilizing everything learned from this sprint in future projects.


   

## C# Live Project using .NET Framework


