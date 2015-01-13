---
title: Form Validation with Flask-WTF
layout: post
---

Recently I made a site which had a form with, amongst other things, latitude
and longitude coordinates as an input.

```python
class InputDataForm(Form):

    lat = FloatField('Latitude', default=-30, 
                     validators=[validators.InputRequired()]) 
    lon = FloatField('Longitude', default=150, 
                     validators=[validators.InputRequired()])
```

I am using a simple validator for making sure that something is input into the
form. But, I also want to make sure that the coordinates fall within a polygon,
which requires access to both field values, and hence cannot be written as a
normal field validator. I have to add custom validation functionality to the
whole form. Flask-WTF lets me do this by overriding the validate method on the
InputDataForm class.

```python
def validate(self):
    def is_in_a_region(lat, lon, regions):
        p = Point(lon, -abs(lat))
        for r in regions:
            if p.within(r.to_shapely()):
                return True
        return False

    rv = Form.validate(self)
    if not rv:
        return False

    regions = Region.query.all()
    if not is_in_a_region(self.lat.data, self.lon.data, regions):
        self.lat.errors.append('Invalid coordinates')
        self.lon.errors.append('Invalid coordinates')
        return False
    return True
```

The `is_in_a_region` function is a bit unwieldy here, since I am not using a
spatially aware database (like PostgreSQL/PostGIS) but plain SQLite with a
string field for storing the geometry as WKT. Still, it does the job.
