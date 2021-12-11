# Tech-Academy-Projects
While studying at The Tech Academy, I completed several assignments and worked on multiple projects in order to build my skillset and proficiency in HTML, CSS, JavaScript, Python, Django, SQL, C# and the .NET framework. I was taught how to think like a programmer in order to find creative solutions while writing clean and precise commented code. Completing these assignments and projects taught me several programming skills and gives me the confidence that I can learn any language or framework fairly quickly.

## Python Live Project
After completing the Python course, I participated in a two week sprint. I was tasked with using Python within the Django framework to create a dynamic web application. I chose travel as my topic and I built a destinations website that allows a user to create, review, update and delete information about their favorite travel destinations. I used several functions in the views in order to retrieve data and display them on the applicable HTML template. Additionally, I connected an API and wrote a basic JSON response that allows the user to view the current temperature at that specific destination. Ideally, I would have utilized data scraping and API's to display the current flight price, which I plan to implement in the future. 

### Creating the Basic App
To start, I created a new application within the Django framework. I created base and home templates and then added function to the views in order for a homepage with a navbar to render. I then registered my URL's and linked my application to the main project home page.

### Creating the Model and Form
I created an object model class with a manager anmd defined it's attributes. 

    class destination(models.Model):
        TripName = models.CharField(max_length=30, default="", blank=False, null=False)
        City = models.CharField(max_length=20, default="", blank=False, null=False)
        State = models.CharField(max_length=20, choices=StateChoices, blank=True)
        Country = models.CharField(max_length=20, default="", blank=True, null=False)
        Notes = models.TextField(max_length=300, default="Notes", blank=True)

        # assigns a manager
        destination = models.Manager()

I then created a model form that will include any inputs the user needs to make.

    from django.forms import ModelForm
    from .models import destination

    class DestinationForm(ModelForm):
        class Meta:
            model = destination
            fields = '__all__'
            
Additionally, I used the following views function to render the create page and utilize the model form to save the item to a database.

    def TravelDestinations_add(request):
    form = DestinationForm(data=request.POST or None)
    if request.method == 'POST':
        if form.is_valid():
            form.save()
            return redirect('TravelDestinations_add.html')
    content = {'form': form}
    return render(request, 'TravelDestinations/TravelDestinations_add.html', content)
    
The following function pulls all current database records but only displays the trip name to the HTML template

    def destinations(request):
    trips = destination.destination.all()
    content = {'trips': trips}
    return render(request, 'TravelDestinations/TravelDestinations_destinations.html', content)
   

## C# Live Project using .NET Framework


