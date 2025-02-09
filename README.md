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
- `PPI90s_ebay`: average market price for a certain X-Man on eBay for issues on _Very Good Condition_ published after 1990;

7. exported dataframes into csv ready for upload in Data viz tool.

### Data Vizs 
1. represent the change in percentage of presence from the 80s to the 90s with a side-by-side <ins>horizontal stack bar chart:
- those with an increase of presence were highlighted.

2. show female X-Men's average price over time in two separate scatterplot.
- x-axis: Average price per issue published in the 80s and the 90s. 
- y-axis: Percentage of Appearance for each X-Men character in issues published in the 80s and the 90s. 

## Limitations & Things I'd Like to Improve
1. This is a data-driven project done within one week - I would like to conduct an in-depth research into Jean Grey.
2. The dataset also listed average prices on various auction sites such as heritage. A comparison between price difference for each character on different sites could be also interesting. 
3. While more and more female superheros emerge, how their value in second-hand market is different from male X-Men's is worth analyzing. 