{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Final Project Submission\n",
    "\n",
    "Please fill out:\n",
    "* Student name: \n",
    "* Student pace: self paced / part time / full time\n",
    "* Scheduled project review date/time: \n",
    "* Instructor name: \n",
    "* Blog post URL:\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "metadata": {},
   "outputs": [],
   "source": [
    "import os, glob\n",
    "import pandas as pd\n",
    "import numpy as np\n",
    "import matplotlib.pyplot as plt\n",
    "import matplotlib.ticker as tick\n",
    "import seaborn as sns"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 24,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "['zippedData\\\\bom.movie_gross.csv.gz',\n",
       " 'zippedData\\\\imdb.name.basics.csv.gz',\n",
       " 'zippedData\\\\imdb.title.akas.csv.gz',\n",
       " 'zippedData\\\\imdb.title.basics.csv.gz',\n",
       " 'zippedData\\\\imdb.title.crew.csv.gz',\n",
       " 'zippedData\\\\imdb.title.principals.csv.gz',\n",
       " 'zippedData\\\\imdb.title.ratings.csv.gz',\n",
       " 'zippedData\\\\rt.movie_info.tsv.gz',\n",
       " 'zippedData\\\\rt.reviews.tsv.gz',\n",
       " 'zippedData\\\\tmdb.movies.csv.gz',\n",
       " 'zippedData\\\\tn.movie_budgets.csv.gz']"
      ]
     },
     "execution_count": 24,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "os.listdir(\"zippedData/\")\n",
    "files = glob.glob(\"zippedData/*\")\n",
    "files"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Studio, Gross & Year Dataset"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 25,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>title</th>\n",
       "      <th>studio</th>\n",
       "      <th>domestic_gross</th>\n",
       "      <th>foreign_gross</th>\n",
       "      <th>year</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <td>0</td>\n",
       "      <td>Toy Story 3</td>\n",
       "      <td>BV</td>\n",
       "      <td>415000000.0</td>\n",
       "      <td>652000000</td>\n",
       "      <td>2010</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <td>1</td>\n",
       "      <td>Alice in Wonderland (2010)</td>\n",
       "      <td>BV</td>\n",
       "      <td>334200000.0</td>\n",
       "      <td>691300000</td>\n",
       "      <td>2010</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <td>2</td>\n",
       "      <td>Harry Potter and the Deathly Hallows Part 1</td>\n",
       "      <td>WB</td>\n",
       "      <td>296000000.0</td>\n",
       "      <td>664300000</td>\n",
       "      <td>2010</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <td>3</td>\n",
       "      <td>Inception</td>\n",
       "      <td>WB</td>\n",
       "      <td>292600000.0</td>\n",
       "      <td>535700000</td>\n",
       "      <td>2010</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <td>4</td>\n",
       "      <td>Shrek Forever After</td>\n",
       "      <td>P/DW</td>\n",
       "      <td>238700000.0</td>\n",
       "      <td>513900000</td>\n",
       "      <td>2010</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <td>3382</td>\n",
       "      <td>The Quake</td>\n",
       "      <td>Magn.</td>\n",
       "      <td>6200.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>2018</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <td>3383</td>\n",
       "      <td>Edward II (2018 re-release)</td>\n",
       "      <td>FM</td>\n",
       "      <td>4800.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>2018</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <td>3384</td>\n",
       "      <td>El Pacto</td>\n",
       "      <td>Sony</td>\n",
       "      <td>2500.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>2018</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <td>3385</td>\n",
       "      <td>The Swan</td>\n",
       "      <td>Synergetic</td>\n",
       "      <td>2400.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>2018</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <td>3386</td>\n",
       "      <td>An Actor Prepares</td>\n",
       "      <td>Grav.</td>\n",
       "      <td>1700.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>2018</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>3387 rows × 5 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "                                            title      studio  domestic_gross  \\\n",
       "0                                     Toy Story 3          BV     415000000.0   \n",
       "1                      Alice in Wonderland (2010)          BV     334200000.0   \n",
       "2     Harry Potter and the Deathly Hallows Part 1          WB     296000000.0   \n",
       "3                                       Inception          WB     292600000.0   \n",
       "4                             Shrek Forever After        P/DW     238700000.0   \n",
       "...                                           ...         ...             ...   \n",
       "3382                                    The Quake       Magn.          6200.0   \n",
       "3383                  Edward II (2018 re-release)          FM          4800.0   \n",
       "3384                                     El Pacto        Sony          2500.0   \n",
       "3385                                     The Swan  Synergetic          2400.0   \n",
       "3386                            An Actor Prepares       Grav.          1700.0   \n",
       "\n",
       "     foreign_gross  year  \n",
       "0        652000000  2010  \n",
       "1        691300000  2010  \n",
       "2        664300000  2010  \n",
       "3        535700000  2010  \n",
       "4        513900000  2010  \n",
       "...            ...   ...  \n",
       "3382           NaN  2018  \n",
       "3383           NaN  2018  \n",
       "3384           NaN  2018  \n",
       "3385           NaN  2018  \n",
       "3386           NaN  2018  \n",
       "\n",
       "[3387 rows x 5 columns]"
      ]
     },
     "execution_count": 25,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df0 = pd.read_csv(files[0])\n",
    "df0"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 26,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "RangeIndex: 3387 entries, 0 to 3386\n",
      "Data columns (total 5 columns):\n",
      "title             3387 non-null object\n",
      "studio            3382 non-null object\n",
      "domestic_gross    3359 non-null float64\n",
      "foreign_gross     2037 non-null object\n",
      "year              3387 non-null int64\n",
      "dtypes: float64(1), int64(1), object(3)\n",
      "memory usage: 132.4+ KB\n"
     ]
    }
   ],
   "source": [
    "df0.info()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Release Dates, Budgets, Gross Dataset\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 27,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>id</th>\n",
       "      <th>release_date</th>\n",
       "      <th>movie</th>\n",
       "      <th>production_budget</th>\n",
       "      <th>domestic_gross</th>\n",
       "      <th>worldwide_gross</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>Dec 18, 2009</td>\n",
       "      <td>Avatar</td>\n",
       "      <td>$425,000,000</td>\n",
       "      <td>$760,507,625</td>\n",
       "      <td>$2,776,345,279</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <td>1</td>\n",
       "      <td>2</td>\n",
       "      <td>May 20, 2011</td>\n",
       "      <td>Pirates of the Caribbean: On Stranger Tides</td>\n",
       "      <td>$410,600,000</td>\n",
       "      <td>$241,063,875</td>\n",
       "      <td>$1,045,663,875</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <td>2</td>\n",
       "      <td>3</td>\n",
       "      <td>Jun 7, 2019</td>\n",
       "      <td>Dark Phoenix</td>\n",
       "      <td>$350,000,000</td>\n",
       "      <td>$42,762,350</td>\n",
       "      <td>$149,762,350</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <td>3</td>\n",
       "      <td>4</td>\n",
       "      <td>May 1, 2015</td>\n",
       "      <td>Avengers: Age of Ultron</td>\n",
       "      <td>$330,600,000</td>\n",
       "      <td>$459,005,868</td>\n",
       "      <td>$1,403,013,963</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <td>4</td>\n",
       "      <td>5</td>\n",
       "      <td>Dec 15, 2017</td>\n",
       "      <td>Star Wars Ep. VIII: The Last Jedi</td>\n",
       "      <td>$317,000,000</td>\n",
       "      <td>$620,181,382</td>\n",
       "      <td>$1,316,721,747</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <td>5777</td>\n",
       "      <td>78</td>\n",
       "      <td>Dec 31, 2018</td>\n",
       "      <td>Red 11</td>\n",
       "      <td>$7,000</td>\n",
       "      <td>$0</td>\n",
       "      <td>$0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <td>5778</td>\n",
       "      <td>79</td>\n",
       "      <td>Apr 2, 1999</td>\n",
       "      <td>Following</td>\n",
       "      <td>$6,000</td>\n",
       "      <td>$48,482</td>\n",
       "      <td>$240,495</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <td>5779</td>\n",
       "      <td>80</td>\n",
       "      <td>Jul 13, 2005</td>\n",
       "      <td>Return to the Land of Wonders</td>\n",
       "      <td>$5,000</td>\n",
       "      <td>$1,338</td>\n",
       "      <td>$1,338</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <td>5780</td>\n",
       "      <td>81</td>\n",
       "      <td>Sep 29, 2015</td>\n",
       "      <td>A Plague So Pleasant</td>\n",
       "      <td>$1,400</td>\n",
       "      <td>$0</td>\n",
       "      <td>$0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <td>5781</td>\n",
       "      <td>82</td>\n",
       "      <td>Aug 5, 2005</td>\n",
       "      <td>My Date With Drew</td>\n",
       "      <td>$1,100</td>\n",
       "      <td>$181,041</td>\n",
       "      <td>$181,041</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>5782 rows × 6 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "      id  release_date                                        movie  \\\n",
       "0      1  Dec 18, 2009                                       Avatar   \n",
       "1      2  May 20, 2011  Pirates of the Caribbean: On Stranger Tides   \n",
       "2      3   Jun 7, 2019                                 Dark Phoenix   \n",
       "3      4   May 1, 2015                      Avengers: Age of Ultron   \n",
       "4      5  Dec 15, 2017            Star Wars Ep. VIII: The Last Jedi   \n",
       "...   ..           ...                                          ...   \n",
       "5777  78  Dec 31, 2018                                       Red 11   \n",
       "5778  79   Apr 2, 1999                                    Following   \n",
       "5779  80  Jul 13, 2005                Return to the Land of Wonders   \n",
       "5780  81  Sep 29, 2015                         A Plague So Pleasant   \n",
       "5781  82   Aug 5, 2005                            My Date With Drew   \n",
       "\n",
       "     production_budget domestic_gross worldwide_gross  \n",
       "0         $425,000,000   $760,507,625  $2,776,345,279  \n",
       "1         $410,600,000   $241,063,875  $1,045,663,875  \n",
       "2         $350,000,000    $42,762,350    $149,762,350  \n",
       "3         $330,600,000   $459,005,868  $1,403,013,963  \n",
       "4         $317,000,000   $620,181,382  $1,316,721,747  \n",
       "...                ...            ...             ...  \n",
       "5777            $7,000             $0              $0  \n",
       "5778            $6,000        $48,482        $240,495  \n",
       "5779            $5,000         $1,338          $1,338  \n",
       "5780            $1,400             $0              $0  \n",
       "5781            $1,100       $181,041        $181,041  \n",
       "\n",
       "[5782 rows x 6 columns]"
      ]
     },
     "execution_count": 27,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df10 = pd.read_csv(files[10])\n",
    "df10"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 28,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "RangeIndex: 5782 entries, 0 to 5781\n",
      "Data columns (total 6 columns):\n",
      "id                   5782 non-null int64\n",
      "release_date         5782 non-null object\n",
      "movie                5782 non-null object\n",
      "production_budget    5782 non-null object\n",
      "domestic_gross       5782 non-null object\n",
      "worldwide_gross      5782 non-null object\n",
      "dtypes: int64(1), object(5)\n",
      "memory usage: 271.2+ KB\n"
     ]
    }
   ],
   "source": [
    "df10.info()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Thesis Questions\n",
    "\n",
    "- Do successful movies trend more towards foreign or domestic markets? (Mean Domestic VS Mean Foreign)\n",
    "    - domestic_gross\n",
    "    - foreign_gross\n",
    "    - Extra - Profit(Gross - Budget, Mean of Difference)\n",
    "\n",
    "- production_budget against worldwide_gross (If I spend more money will it make more money)\n",
    "    - production_budget\n",
    "    - worldwide_gross\n",
    "    \n",
    "- Is there a studio that seems to attract a certain level of success?\n",
    "    - Studios\n",
    "    - Mean worldwide gross\n",
    "    - Extra - Profit(Gross - Budget, Mean of Difference, list             against studio)\n",
    "- Is there an amount spend in the budget that studios don't exceed OR Is there a direct relationship to amount spent in production Vs. How much is actually made?|"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Approach\n",
    "- We want to be profitable and make money\n",
    "    Comparing production costs to gross costs to see if there is any trend between money spent and money earned. Is there more money to be made in the domestic zone, foreign zone or both? Analyzing how other studios handle their investments and what works well for them, what is the tried and tested model and how can we replicate that?\n",
    "    - "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Mean Domestic Vs. Mean Foreign\n",
    "    - Foreign markets are lucative\n",
    "    - Domestic is safe\n",
    "    - Find something that both these groups would like to see"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 29,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "28745845.06698422\n",
      "74872810.15046637\n",
      "72.25804078748256\n",
      "27.741959212517443\n"
     ]
    }
   ],
   "source": [
    "#Mean for Domestic\n",
    "domestic_gross_mean = df0['domestic_gross'].mean()\n",
    "print(domestic_gross_mean)\n",
    "\n",
    "#Mean for Foreign\n",
    "df0['foreign_gross'] = df0['foreign_gross'].astype('str')\n",
    "\n",
    "df0['foreign_gross'] = df0['foreign_gross'].str.replace(',', '').astype(float)\n",
    "\n",
    "foreign_gross_mean = df0['foreign_gross'].mean()\n",
    "print(foreign_gross_mean)\n",
    "\n",
    "#Domestic minus Foreign/Foreign minus Domestic\n",
    "foreign_gross_mean - domestic_gross_mean\n",
    "\n",
    "foreign_mean_percentage = 100 * foreign_gross_mean/(foreign_gross_mean + domestic_gross_mean)\n",
    "domestic_mean_percentage = 100 * domestic_gross_mean/(foreign_gross_mean + domestic_gross_mean)\n",
    "print(foreign_mean_percentage)\n",
    "print(domestic_mean_percentage)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 30,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "labels = 'Foreign Gross Mean', 'Domestic Gross Mean'\n",
    "sizes = [foreign_mean_percentage, domestic_mean_percentage]\n",
    "fig1, ax1 = plt.subplots()\n",
    "ax1.pie(sizes, labels=labels, autopct='%1.2f%%')\n",
    "ax1.axis('equal')\n",
    "plt.title('Gross Distribution Foriegn/Domestic Films ')\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Production Budget Vs. Worldwide Gross\n",
    "    - Positive trend\n",
    "    - If we spend more, we're likely to make more"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 31,
   "metadata": {
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "#Sum of Production Expenditures\n",
    "df10['production_budget'] = df10['production_budget'].astype('str')\n",
    "df10['production_budget'] = df10['production_budget'].str.replace('$', '')\n",
    "df10['production_budget'] = df10['production_budget'].str.replace(',', '').astype(float)\n",
    "\n",
    "#Worldwide Gross\n",
    "df10['worldwide_gross'] = df10['worldwide_gross'].astype('str')\n",
    "df10['worldwide_gross'] = df10['worldwide_gross'].str.replace('$', '')\n",
    "df10['worldwide_gross'] = df10['worldwide_gross'].str.replace(',', '').astype(float)\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 32,
   "metadata": {},
   "outputs": [],
   "source": [
    "# Code Sourced from \"https://dfrieds.com/data-visualizations/how-format-large-tick-values.html\"\n",
    "def reformat_large_tick_values(tick_val, pos):\n",
    "    \"\"\"\n",
    "    Turns large tick values (in the billions, millions and thousands) such as 4500 into 4.5K and also appropriately turns 4000 into 4K (no zero after the decimal).\n",
    "    \"\"\"\n",
    "    if tick_val >= 1000000000:\n",
    "        val = round(tick_val/1000000000, 1)\n",
    "        new_tick_format = '{:}B'.format(val)\n",
    "    elif tick_val >= 1000000:\n",
    "        val = round(tick_val/1000000, 1)\n",
    "        new_tick_format = '{:}M'.format(val)\n",
    "    elif tick_val >= 1000:\n",
    "        val = round(tick_val/1000, 1)\n",
    "        new_tick_format = '{:}K'.format(val)\n",
    "    elif tick_val < 1000:\n",
    "        new_tick_format = round(tick_val, 1)\n",
    "    else:\n",
    "        new_tick_format = tick_val\n",
    "\n",
    "    # make new_tick_format into a string value\n",
    "    new_tick_format = str(new_tick_format)\n",
    "    \n",
    "    # code below will keep 4.5M as is but change values such as 4.0M to 4M since that zero after the decimal isn't needed\n",
    "    index_of_decimal = new_tick_format.find(\".\")\n",
    "    \n",
    "    if index_of_decimal != -1:\n",
    "        value_after_decimal = new_tick_format[index_of_decimal+1]\n",
    "        if value_after_decimal == \"0\":\n",
    "            # remove the 0 after the decimal point since it's not needed\n",
    "            new_tick_format = new_tick_format[0:index_of_decimal] + new_tick_format[index_of_decimal+2:]\n",
    "            \n",
    "    return new_tick_format\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 33,
   "metadata": {},
   "outputs": [],
   "source": [
    "#Oldest to Newest\n",
    "df10['release_date'] = df10['release_date'].astype('str')\n",
    "pd.to_datetime(pd.Series(df10['release_date']))\n",
    "df10.sort_values(by=['release_date'], inplace=True)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 34,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.lineplot(x = df10['production_budget'], y = df10['worldwide_gross'])\n",
    "plt.xlabel(\"Production Budget\", labelpad=16)\n",
    "plt.ylabel(\"Worldwide Gross\", labelpad=16)\n",
    "plt.title(\"Budget/Gross Trend Relationship\", y=1.02, fontsize=22)\n",
    "ax = plt.gca()\n",
    "ax.xaxis.set_major_formatter(tick.FuncFormatter(reformat_large_tick_values));\n",
    "ax.yaxis.set_major_formatter(tick.FuncFormatter(reformat_large_tick_values));\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Movies by Release Date & Worldwide Gross"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 35,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "image/png": "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TFGUsMjJyeHEE09UBXMEIiKceOKJYfViVckoihI2qmCOXMJ996pkFB92ZeZQ783RTF61M9aiKIpSAVAlo/iwbOt+AP6YHXBelaLEnJdffplvvvnGe9ymTRueeOIJ7/Grr77KV199FVaeNWvWDBjeoUMHBg0a5CqPLl26MHHixCLhU6dOpW3btmHJs3btWtq2bcs555zDJZdcwrXXXsv06dPDyiNeUCWjKEq54oorriAxMRGAwsJC0tLSWL58uTc+MTGRK6+80lVeBQUFEZPr/fff54Ybbih1Pjk5Odx666089dRTrF+/nqSkJL777js2bNhQJG1+fn6prxdt1LtMUZQS897I5azYlhHRPBvWPYZ3b2sUNP7KK6/k5ZdfBmD58uU0btyY7du3s2/fPo466ihWrlzJRRddhDGGzp07M3bsWESEt99+m/bt2zN16lTee+89Tj31VJKTk1mxYoU3b2MML7zwApMnT+ass87Csz39vHnz+PTTTxkyZAjDhw/n/vvvZ//+/RQWFtKwYUM2bNhAhw4daNu2Le3atWPcuHF06tSJ2rVrc/HFF3vzz87O5oUXXmDp0qXk5+fTtWtX7rjjDp/769u3Ly1btuT222/3hjVu3JjGjRsD0LVrV7Zt20ZKSgq1a9emV69ePPvssyxYsIAqVarw1Vdfce2117J8+XI6duxIbm4uhYWFDB48mLp163LfffeRmppKQUEB77zzDu3bty/9SwuBKhlFUcoVdevWpUqVKmzevJnExERatmzJ1q1bmT17NsceeyxNmzalWrVqDB48mOTkZBYvXkxaWhqXXnopV199NWApjWXLlhVxwx06dCirV69m6dKl7Ny5k4YNG/LYY49x8cUXs2jRIgBmzJhB48aNmT9/Pvn5+bRo0cInj5ycHJ588kkmT57Mueee61OJf/TRR1x33XX06tWL9PR0LrvsMm644QaOPvpob5rly5f7KKZAJCUlMXPmTBISEvjyyy8BWLp0KatWreLGG29kzZo1/PTTT7z00ks89NBD5ObmUlBQwJgxY6hbty6jR48GYP/+/SV8C+5RJaMoSokJ1eOIJldeeSWJiYkkJibyyiuvsHXrVhITEzn22GO54oorAJg5cyYPPPAAlStX5uSTT+aaa65h/vz5HHPMMVx22WUB53lMnz7de07dunW57rrrAKhSpQrnnnsuK1eu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kJub6/0d7JxAhLp21apVvXlVrly52C2URYTbbruN7777jjfffDOojMHuK5Qsnq0Hzj//fJ/wuXMDteVLRlybywBEpCqWgulrjBniH2+MyTDGZNm/xwBVRaR2gHSzgdpAnSiLrChKHNCiRQumTZtGWloaBQUF9OvXj2uuuYYWLVowdepU9uzZQ15eHgMHDvSeU69ePZKSkgAYPnw4eXl5ANx444306tXL6+Hl2dulVq1aZGZmur52SZk5cybnnHNOSBmDbVPQoEEDNmzYQEpKCoCPA0GwrQeC3VdJiGslI5Za7gmsNMZ8FSTNKXY6ROQyrHvaEyBdA6ByoDhFUSoep556Kp988gnXXnstF154IRdffDF33HEHp556Kl27dqVly5bccMMNPlsdP/nkk0ybNo3LLruMuXPnentGN910E7fffjvNmzenWbNmXvNShw4deOaZZ2jWrBkHDx4s9trh4BmTadq0KYsWLeKdd94JKeNdd93l3f3y2Wef9Sq1hIQEfvjhB2666SZatWrFySefzLHHHgtYWw/k5eXRtGlTGjdu7L3Gtddey4oVK2jWrFmpvdrieql/EWkFzACWAh5/xH8DZwAYY34SkeeBZ7E80Q4CrxhjEu3zC+xzAQT4tzFmdKhr6lL/utS/Ehpd6r/8kZWVRc2aNb3jO/Xr1+fll18ucX7hLPUf12MyxpiZWMohVJrvge+DxFWOhlyKoijliR49evDbb7+Rm5vLRRddxNNPP11m145rJaMoiqKUnpdffrlUPZfSENdjMoqixCfxbGZXoku4716VjKIoYVGjRg327NmjiuYIxBjDnj17qFGjhutz1FymKEpYnH766aSmpvrMHFeOHGrUqMHpp5/uOr0qGUVRwqJq1are2eOKUhxqLlMURVGihioZRVEUJWqoklEURVGihioZRVEUJWqoklEURVGihioZRVEUJWqoklEURVGihioZRVEUJWqoklEURVGihioZJSBTVu/mUH5BrMVQFKWco0pGCcqPU9fHWgRFUco5qmSUoGQczI+1CIqilHNUySiKoihRQ5WMoiiKEjVUySiKoihRQ5WMoiiKEjVUySiKoihRQ5WMoiiKEjVUySiKoihRQ5WMEhSDibUIiqKUc1TJRJj8gkJy8nQ5FkVRFFAlE3Hu+3k2Dd4ZF2sxFEVR4oJyr2RE5B8iMkVEVorIchF5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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.xlabel(\"Movies\", labelpad=16)\n",
    "plt.ylabel(\"Worldwide Gross\", labelpad=16)\n",
    "plt.title(\"Movies & Worldwide Budget/Gross Relationship\", y=1.02, fontsize=22)\n",
    "\n",
    "ax = plt.gca()\n",
    "ax.xaxis.set_major_formatter(tick.FuncFormatter(reformat_large_tick_values));\n",
    "ax.yaxis.set_major_formatter(tick.FuncFormatter(reformat_large_tick_values));\n",
    "df10.plot(kind='line',x='movie',y='worldwide_gross', ax=ax)\n",
    "df10.plot(kind='line',x='movie', y='production_budget', color='red',ax=ax)\n",
    "x_axis = ax.axes.get_xaxis()\n",
    "x_axis.set_visible(False)\n",
    "plt.title('Movies & Worldwide Budget/Gross Relationship')\n",
    "plt.legend(['Worldwide Gross', 'Production Budget'])\n",
    "plt.show()\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Movies by Release Date & Domestic Gross"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 36,
   "metadata": {},
   "outputs": [],
   "source": [
    "#Sum of Production Expenditures\n",
    "df10['production_budget'] = df10['production_budget'].astype('str')\n",
    "df10['production_budget'] = df10['production_budget'].str.replace('$', '')\n",
    "df10['production_budget'] = df10['production_budget'].str.replace(',', '').astype(float)\n",
    "\n",
    "#Worldwide Gross\n",
    "df10['domestic_gross'] = df10['domestic_gross'].astype('str')\n",
    "df10['domestic_gross'] = df10['domestic_gross'].str.replace('$', '')\n",
    "df10['domestic_gross'] = df10['domestic_gross'].str.replace(',', '').astype(float)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 41,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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srOz3dupqan89a9/Zd++fRQUFPD000+zZMkSkpKS+Pjjj7n66qsZPHgwY8eOpaSkhJSUFF599VUKCwv5/vvvqVOnDpMmTaJRo0Zs3ryZZ599loyMDI466igGDBjAWWedxahRo+jRoweJiYk0aNCA6dOn06JFC/Ly8mjSpAldu3YlLy+PJUuW8MUXX7Bnzx46duxIamoqAH379uWyyy5zy7x582auv/56Nm3aREJCRaPSrFmz6NGjByeffDLJycmsWbOGjz/+2K2EHn/8cV566SVycnK49957SU9Pp6SkhG7dutG+fXu6dOnC+PHjSUpK4oYbbuDDDz+MxOsBypcBFyKy1BjTxjut9mQURan2NG/enNLSUvbu3cvQoUMBWLVqFevWreOGG25gw4YNAKSkpLB8+XLy8/Np0aIFvXv3Zvny5bz88ssMGTKEl156iSeffJJ+/frRsmVLFi5cyDPPPMPMmTPp2bMnU6dOpUmTJhw8eJDatWvTs2dPt1IBGDx4sFumF154gSuvvJIxY8ZQUlJSTikCrF69mvPPP9+ngnGxaNEiUlJSOP3001m6dCmDBg1i4cKFGGNo27YtV155JampqZxyyilMnGg1DrOysti/fz9jxoxh3bp1iAgHDx6M5OMOCVUyiqKETbAeR1XissrMnTuX559/HoCzzjqL0047za1krr76aurXr0/9+vVp0KABt912GwCtWrVi5cqVZGdnM3/+fO655x53vgUFBQD87W9/o0OHDtx7773885//DCrPzJkzGTJkCIC79xOId955h1GjRrF371527twJwMUXX+yejzJ37lz+8Y9/cPTRRwPwz3/+k99//52bbrqJTp068frrr9OuXTsuv/xyiouLqVu3Lo8//ji33nor7dq1c/YQo4AO/CuKUu1JTU0lMTGRE088kUBDAHXq1HH/TkhIcG8nJCRQXFxMaWkpDRs2JDk52f23du1aAPr160evXr3Yvn07rVu3JjMzs1Iyn3322axYscLtsPCf//yH5ORkDh0qMz+6FArg977OPPNMli5dSqtWrejatSs9e/YkKSmJRYsWcddddzF27FhuuummSslaGVTJKIpSrcnIyKBjx44899xziAhXXHEFw4YNA2DDhg1s27aNP//5z47yOvbYYzn99NMZNWoUYFXsK1asAKwxlLZt29KzZ09OOOEEtm/fTv369Tl8+LDPvK699lr69u0LWAP3nsoDoEWLFrRp04Y333yTkpISwJro6k+ZXHHFFYwdO5bc3FxycnIYM2YMl19+OTt37uSoo47ioYceolOnTixbtozs7GyysrK45ZZb+PTTT91OErFAzWWKolQ78vLyaN26NUVFRSQlJfHwww/zyiuvAPDMM8/QsWNHWrVqRVJSEoMHDy7XgwnGsGHDePrpp+nVqxdFRUXcd999nH/++XTu3JmNGzdijOHaa6/l/PPP59RTT+X999+ndevWdO3atVw+n332GU8++STffPMNiYmJ9O3bl0svvbRcmoEDB9K5c2datGhBo0aNqFevHr179/Yp14UXXkiHDh24+OKLAWvg/4ILLmDq1Kl07tyZhIQEatWqRd++fTl8+DB33HGHW2l98sknoTzeiKLeZV6od5l6lymB8eVZpBxZhOJdpuYyRVEUJWqoklEURVGihioZRVEUJWqoklEURVGihioZRVEUJWqoklEURVGihioZRVGqHa5Q/+eeey733HMPubm5Yec1ePBgnnvuubDPdYWAAWvuypo1a8KWxTPfxo0bu5czuPvuu0O+xw4dOjB69Oiwru+9hEFlUCWjKEq1wxXqPyUlhdq1a9OvX79yx40xVbK+jLeSGThwIGeffXZE8m7fvj3JycmsXr2a2rVrM3LkyIjk64RIKhmd8a8oSvi89BJEOmRJ69bw6aeOk19++eWsXLmStLQ0br75Zq6++moWLFjA2LFjmT9/Pu+++y7GGG699Vb3bPpBgwbx3nvvcfLJJ3PmmWe6IwJ06NCBdu3acffddwPllxT44IMP+P7770lISODmm2+mTZs2LFmyhAcffJB69eqxYMECbr75Zj788EPatGnD8OHDfV77mGOO4cUXX2TChAnUq1ePcePGcdJJJ/m9v+LiYnJycjjuuOMCymiM4fnnn2fmzJmcfvrp5cLTTJo0iVdeeYUTTjiBCy+8kNTUVCZMmEBOTg7PP/88q1atori4mO7du3PzzTfz1ltvkZeXx9y5c+natSvt27d3/D680Z6MoijVluLiYiZPnkyrVq0AWL9+PY888gjLly+nVq1avP7668ycOZPk5GQWL17M2LFj2bVrF2+//Tbz5s1j2rRpjsxbkydPZuzYsSxcuJAVK1bw2muvcffdd9OmTRuGDRtGcnIy9erVc6ffuXOnz2sD5OTkcMkll7BixQquuOIKvythjhw5ktatW9OkSRP279/vjhjtjzFjxrB+/XpWrVrFgAEDmD/fWkI9Pz+fp556ismTJzN37lwyMjLc57zzzjtcc801LF68mN9++43OnTtTVFREz5493T2pyigY0J6MoiiVIYQeRyRxxS4Dqyfz2GOPsXPnTk477TQuueQSABYvXsxVV11F48aNAXjwwQeZM2cOQLn97du3dy8F4I/p06fzr3/9i6OOOgqARo0aBUzv79p33nkntWvXdofev+iii5g2bZrPPNq3b88XX3yBMYZnn32W//3vf3Tp0sXvNefMmcP9999PYmIip5xyCtdccw0A69ato3nz5u4lA+6//3769+8PwK+//sr48ePdC5rl5+ezbdu2gPcWKqpkFEWpdnguv+yJk9D4ACLic39SUpJ7LMcYQ2Fhofu3v3N8EejatWrVcueVmJhIcXFxwLxEhNtuu40+ffrQpUsXvzL6u69Ashhj+OmnnypEqV64cGFAmUJBzWWKotRI2rZty+zZs9m3bx8lJSUMHz6cK6+8krZt2zJr1iwyMzMpKipyh/UHaNasGUuXLgVg3LhxFBUVAXDDDTfw7bffuj289u/fD+A31L+/a4fL3LlzOeOMMwLKeMUVVzBixAhKSkrYtWsXv/32G2At3JaamkpaWhpAOQeCG2+8kT59+rgV0fLlywPeVzioklEUpUZy8skn895773H11Vdz/vnnc+GFF3LHHXdw8skn0717dy699FKuu+46LrzwQvc5TzzxBLNnz+biiy9m4cKF7p7RTTfdxO23306bNm1o3bq127zUoUMHOnbsSOvWrcnLywt67VBwjcmcd955LF++nG7dugWU8R//+ActW7akVatWPP30026lVq9ePb766ituuukm/v73v3PSSSe5V+ns1q0bRUVFnHfeeZx77rnua1x99dWsWbOG1q1bV9qrTUP9e6Gh/jXUvxIYDfVf/cjOzuaYY45xj++0bNmSl19+Oez8NNS/oiiK4mbAgAHuiZ1ZWVk89dRTVXbtuFIyIvKyiKwWkRQRGS4idUXkdBFZKCIbRWSkiNS209axtzfZx5vZ+68SESMij3nke4G9r1Ns7kxRFCV2vPzyyyQnJ7NmzRqGDRvm9pKrCuJGyYhIE+AFoI0x5lwgEbgP6A18YoxpCRwAXMrjMeCAMaYF8Imd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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.xlabel(\"Movies\", labelpad=16)\n",
    "plt.ylabel(\"Domestic Gross\", labelpad=16)\n",
    "plt.title(\"Movies & Domestic Budget/Gross Relationship\", y=1.02, fontsize=22)\n",
    "\n",
    "ax = plt.gca()\n",
    "ax.xaxis.set_major_formatter(tick.FuncFormatter(reformat_large_tick_values));\n",
    "ax.yaxis.set_major_formatter(tick.FuncFormatter(reformat_large_tick_values));\n",
    "df10.plot(kind='line',x='movie',y='domestic_gross', ax=ax)\n",
    "df10.plot(kind='line',x='movie', y='production_budget', color='red',ax=ax)\n",
    "x_axis = ax.axes.get_xaxis()\n",
    "x_axis.set_visible(False)\n",
    "plt.title('Movies & Domestic Budget/Gross Relationship')\n",
    "plt.legend(['Domestic Gross', 'Production Budget'])\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Studios & Domestic & Foreign Gross"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 38,
   "metadata": {},
   "outputs": [],
   "source": [
    "studio = df0['studio']\n",
    "\n",
    "domestic_gross = df0['domestic_gross']\n",
    "\n",
    "foreign_gross = df0['foreign_gross']\n",
    "\n",
    "df0['foreign_gross'] = df0['foreign_gross'].astype('str')\n",
    "df0['foreign_gross'] = df0['foreign_gross'].str.replace(',', '').astype(float)\n",
    "\n",
    "df0['year'] = df0['year'].astype('str')\n",
    "pd.to_datetime(pd.Series(df0['year']))\n",
    "df0.sort_values(by=['year'], inplace=True)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 39,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.xlabel(\"Studios\", labelpad=16)\n",
    "plt.ylabel(\"Worldwide Gross\", labelpad=16)\n",
    "plt.title(\"Studio & Domestic/Foreign Gross\", y=1, fontsize=22)\n",
    "\n",
    "ax = plt.gca()\n",
    "ax.xaxis.set_major_formatter(tick.FuncFormatter(reformat_large_tick_values));\n",
    "ax.yaxis.set_major_formatter(tick.FuncFormatter(reformat_large_tick_values));\n",
    "df0.plot(kind='line',x='studio',y='foreign_gross', ax=ax)\n",
    "df0.plot(kind='line',x='studio', y='domestic_gross', color='red',ax=ax)\n",
    "plt.title('Studio & Domestic/Foreign Gross')\n",
    "plt.legend(['Foreign Gross', 'Domestic Gross'])\n",
    "plt.show()\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Conclusion\n",
    "- There is growth in the foreign market\n",
    "    - If we can appeal to all peoples and unifying things about our species, we can blow this out of the park\n",
    "- We should build off the back of success that has worked for others studios\n",
    "- Don't spend more than half of what you're expecting to make\n",
    "    - You get what you put in\n",
    "        - Can't expect to make a billion off of a shrimp budget\n",
    "        - Be realistic with your profit goals, don't overextend production budgets."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.6.9"
  },
  "toc": {
   "base_numbering": 1,
   "nav_menu": {},
   "number_sections": true,
   "sideBar": true,
   "skip_h1_title": false,
   "title_cell": "Table of Contents",
   "title_sidebar": "Contents",
   "toc_cell": false,
   "toc_position": {
    "height": "calc(100% - 180px)",
    "left": "10px",
    "top": "150px",
    "width": "343px"
   },
   "toc_section_display": true,
   "toc_window_display": true
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}
