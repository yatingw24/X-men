# The Market Value of Jean Grey Among Female X-Men
X-Men, first made their debut in American Comics in 1963, are a group of mutants - humans with supernatural power that manifested at puberty - that later reached a huge fanbase. 

Here is the shortcut to my [article:](https://yatingw24.github.io/X-men/)

A great thank to [Rally's Mutant Moneyball](https://github.com/EliCash82/mutantmoneyball/tree/main?tab=readme-ov-file), who provided the context for data collection and a walkthrough of his priliminary data analysis.

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
 - `DataWrapper`

### A Break Down of Files:
 - `X-men_analysis.ipynb`: the jupyter notebook where I did my majority of data cleaning and analysis.
 - `febay_output.csv`: average price per X-Man on eBay for issues published in the 80s and the 90s. 
 - `female_output.csv`: each female X-Man's percentage of presence in issues published in 80s and 90s.
 - `x-men.csv`: the original dataset that contains price information on all 26 X-Men characters. 

### Data Cleaning and Analysis 
1. assigned a gender for all 26 X-Men.
2. created a dataframe, `df_female`, which contains all information, issues each is featured in different decades and market value on various audtion sites.
3. separated first names and last names and converted each name into the standard name format.
4. replaced all signs, such as a dollar sign ($) or a percentage sign (%).
5. selected columns, `member`, `90s_Appearance_Percent` and `80s_Appearance_Percent` to see the change in the amount of presence in issues published in the 80s versus the 90s:

- `member`: X-Men's names.
- `90s_Appearance_Percent`: the percentage of appearance in issues published after 1990.
- `80s_Appearance_Percent`: the percentage of appearance in issues published between 1980 and 1989.

6. analyzed the market value of each X-Man by pulling out columns `PPI80s_ebay` and `PPI90s_ebay`:

- `PPI80s_ebay`: average market price for a certain X-Man on eBay for issues on Very Good Condition published between 1980 and 1989;
- `PPI90s_ebay`: average market price for a certain X-Man on eBay for issues on Very Good Condition published after 1990;

7. exported dataframes into csv ready for upload in Data viz tool.

### Data Vizs 
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

## Things I'd like to add/improve:
1. 