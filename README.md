# PandasBasketball
PandasBasketball is a small module intended to scrape data from [basketball-reference](https://www.basketball-reference.com/) and convert it to useful pandas data structures, such as data frames, for future analytical purposes. The use of jupyter notebooks is encouraged.

# Installation
There's really no installation per se, just download the folder named 'PandasBasketball' and place it on the directory where you will be using the jupyter notebook. That's it.
You can then import it to your jupyter environment:
```
from PandasBasketball import pandasbasketball as pb
```

## Requirements
Please make sure you meet the following rquirements:
- Python 3.6+
- requests
- pandas
- Beautiful Soup 4

All the requirements can be met easily with the installation of the [Anaconda](https://www.anaconda.com/download/) distribution.

# Usage
## Players
Inside a player's page on the basketball-reference website you can find several tables, and most of these tables can be obtained as a pandas data frame by calling `get_player(code, stat)`. The 'code' refers to the name of the html file used by basketball-reference inside the url, and the 'stat' means the kind of table.
For example, if you wish to obtain the table 'Per Game' of LeBron James you can simply type `pb.get_player("jamesle01", "per_game")` since the full url is https://www.basketball-reference.com/players/j/jamesle01.html.
The currently supported tables are:
- Per Game (`per_game`)
- Totals (`totals`)
- Per 36 Minutes (`per_minute`)
- Per 100 Poss (`per_poss`)
- Advanced (`advanced`)
- Playoffs Per Game (`playoffs_per_game`)
- Playoffs Totals (`playoffs_totals`)
- Playoffs Per 36 Minutes (`playoffs_per_minute`)
- Playoffs Per 100 Poss (`playoffs_per_poss`)
- Playoffs Advanced (`playoffs_advanced`)

The rest of the tables will come in the future.

## Considerations
- The resulting data frame will have the same column names as the table's header but it will not have a set index.
- The resulting data frame **does not** include the table's footer.
- The columns will be of type 'object', so in order to perform arithmetic functions on them you will need to convert them to numeric. You can do something like this:
```
lbj_pg = pb.get_player("jamesle01", "per_game")
lbj_pg[lbj_pg.columns] = lbj_pg[lbj_pg.columns].apply(pd.to_numeric, errors="ignore")
```

# Known issues
TODO: Add known issues