from django.shortcuts import render, get_object_or_404
from .models import (
    Category,
    Location,
    JobListing
)

# Create your views here.
def home(request):
	country = Location.objects.all()
	context = {'country': country}
	return render(request, "dubai_job/index.html", context)

def areas(request, country_id):
	job = get_object_or_404(Location, id=country_id)
	joblist = job.joblisting_set.order_by('-date_added')
	context = {'job': job, 'joblist': joblist}
	return render(request, "dubai_job/location.html", context)

#def type(request, cat_id):
#	jobs = get_object_or_404(Category, id=cat_id)
#	cat_listing = jobs.entry_set.order_by('-date_added')
#	context = {'jobs': jobs, 'cat_listing': cat_listing}
#	return render(request, 'dubai_job/type.html', context)
