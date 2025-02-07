# The Market Value of Jean Grey Among Female X-Men
X-Men, first made their debut in American Comics in 1963, are a group of mutants - humans with supernatural power that manifested at puberty - that later reached a huge fanbase. 

Here is the shortcut to my [article:](https://yatingw24.github.io/X-men/)

A great thank to [Rally's Mutant Moneyball](https://rallyrd.com/mutant-moneyball-a-data-driven-ultimate-x-men/?), who provided the context for data collection and a walkthrough of his priliminary data analysis.

## Key Takeaways of my Project
Jean Grey, heavily referenced in both American comics and the film franchise, remains valuable in the second-hand market;

Readers love a dramatic twist - the death of Jean Grey in 1980 has only made her more sought-after than any female X-Man;

Jean Grey's legacy is passed onto her daughter, Rachel Summers, who saw a highest price for on eBay. 

## Goal:
understanding the shift in the market value of female X-Men by comparing their percentage of appearance in the 80s vs. the 90s and average personal price on auction websites such as eBay.\

Questions that this article aims to answer:
1. what drives the disappearance, or the resurgence, of a female character?
2. in which era does X-Men of more diverse background came into play?
3. as more characters were created, does the core members need to make more space for them?
4. how willingly do collectors of X-Men issues are to pay for a premium for rare issues and rare characters?
5. are female X-Men in the 80s just auxiliary?

## What I Did:
### Tech stack used:
 - `python - pandas`
 - `regex`
 - `csv` 

### Cleaning and Filtering Data
1. open the csv file, remove all null values and re-order the countries in which those without any data are moved to the bottom in pandas;
2. exported the cleaned DataFrame as `ages.csv`:

### Adding URLS 
1. created the `app.py` file, adding the homepage route:
```python
@app.route("/")
def age_at_marriage():

    df = pd.read_csv("ages.csv")
    ages = df.to_dict('records')

    ages=ages
```
2. building the html template `age_at_marriage.html`;
```python
<body>
    <h1>Age at First Marriage Across Countries</h1>
```
3. rendering it to a full web page: 
```python 
return render_template(
    'age_at_marriage.html')

```

### Adding More Pages and Content
#### `Country` as a filter
now, we want pages for each country, right?
So I built another route, `age_at_marriage/<country_name>` and another template, `individual_age.html`.
The logic is pretty simple here:
```python
<h1>In {{country['Country']}}, the average age at first marriage for...</h1>
<h2>
    {% if country['Female'] != "not available" %}
        Female's age at her first marriage is {{country['Female'] |int}} years old.
    {% else %}
        Data for female's age at first marriage is not available, sorry. 
    {% endif %}
</h2>
```
If an integer, aka `the age`, is unavilable for a country, then a `not available` will be returned:  
```python
<h2>
    {% if country['Male'] != "not available"  %}
        Male's age at his first marriage {{country['Male'] |int}} years old.
    {% else %}
        Data for male's age at first marriage is not available, sorry. 
    {% endif %}
</h2>
```
#### `Gender` as a filter
Due to time constraint towards the end of semester, I was't able to add gender as a secondary condition/filter. However, I did try to add a new route which is similar to the `@app.route("/<country_name>")` route:

```python 
@app.route("/<gender>", methods=["GET"])
def age_by_gender(gender):
    df = pd.read_csv("ages.csv")

    gender = request.args.get("gender")
```
An user is able to look up a sepcific gender's data for all countries: 
```python
    
if gender == "Female":
    age = df[['Country', 'Female']]
elif gender == "Male":
    age = df[['Country', 'Male']]

ages = ages.to_dict('records')
return render_template('select_gender.html', gender=gender, ages=ages)
```

the presentable format is a table. In my template, `select_gender.html', I first set up each column's name:
```python
<tr>
    <th>Country</th>
    <th>Age at First Marriage for {{ gender }}</th>
</tr>
```

then, looping through each country's data for the selected gender:
```python

{% for entry in ages %}
    <tr>
        <td>{{ entry['Country'] }}</td>
        <td>
            {% if entry[gender] != 'not available' %}
                {{ entry[gender] }} years
            {% else %}
                Data not available
            {% endif %}
        </td>
    </tr>
{% endfor %}
```
### Linking everything
To link everything, I went back to my `app.py`. I added and adjusted a few more lines of codes:

```python
country = request.args.get("country_name")
select_gender = request.args.get("gender")
```

If a user specifies a `country_name`, the app searches for matching rows in the data and returns details for that `country`:
```python
    if country:
        matching_rows = df[df['Country'] == country]
        country=matching_rows.to_dict("records")[0]
        
        return render_template('individual_age.html',
                               country = country
                               )
``` 
If a user specifies a `gender`, the app searches for matching rows in the data and returns details for that `gender':
```python
        age=age.to_dict('records')
        return render_template('select_gender.html',
                                   gender=select_gender,
                                   ages=age)
```

## Things I'd like to add/improve:
1. insert a chart showing gender difference for each country;\
2. use gender as a secondary filter  to exactly pinpoint a specific gender's age in a specific country;\
3. If possible, I'd like my app to autogenerate a chart for comparision purposes if an user would like to see the age difference for females in two countries.