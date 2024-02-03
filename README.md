# ProjectSlipstream
![ProjectSlipstream Project Image](/_readme_images/ProjectSlipstream.png "ProjectSlipstream Project Image")

## Project description and features
* ProjectSlipstream is a data science project. It uses vehicle lists from every (as of writing) released game in the Forza series of racing games to create a dataset.
* It involves multiple steps:
    1. Use the MediaWiki API to extract the wiki markup.
    2. Perform data extraction and processing.
    3. Placing the processed data into a Pandas DataFrame, with the option of saving it in a ``.csv`` file.
    4. Performing data visualisation.
* I made this project to gather further insights and learn more about the racing games that I enjoy playing.

## Commands (Shell)
### Virtual environment installation:
* Windows (cmd, ps):
    ```
    sh/install.cmd
    ```
* Mac/Linux (bash):
    ```
    sh sh/install.sh
    ```
### Running the notebook: 
* Windows (cmd, ps):
    ```
    sh/run.cmd
    ```
* Mac/Linux (bash):
    ```
    sh sh/run.sh
    ```

## Commands (Manual) 
### Virtual environment installation:
1. 
    ```
    python -m venv venv
    ```
2.  If using bash:
    ```
    source venv/Scripts/activate
    ```

    If not using bash:
    ```
    venv/Scripts/activate
    ```
3. 
    ```
    pip install jupyterlab pandas pyarrow plotly pycountry
    ```

### Running the notebook: 
1. Activate the virtual environment:

    If using bash:
    ```
    source venv/Scripts/activate
    ```
    
    If not using bash:
    ```
    venv/Scripts/activate
    ```
2. Use either:
    Jupyter Lab (recommended):
    ```
    jupyter lab
    ```
    or Jupyter Notebook:
    ```
    jupyter notebook
    ```

## Notes: 
* I do admit that a public wiki is not an ideal data source. If an official API that provided the same data was available, it would be used instead.
* To address common risks of public wiki data:
    * Data can be inaccurate 
        * The Forza wiki vehicle lists appear to be reasonably accurate. By referring to other sources such as gameplay footage and first-party information, several vehicles mentioned in the lists do appear in their respective games with accurate statistic values. 
        * It can be assumed that the data was collected by playing each game and recording each vehicle and its statistics. 
        * Since references are not provided for every vehicle list, and the collection method isn't exactly known, the accuracy is not completely guaranteed. 
        * If any inaccuracies are found, they can be easily fixed by editing the wiki page.
    * Data can be inconsistently formatted and the markup structure can change
        * Formatting and structure can be a hard aspect to predict when working with markup data. 
        * Several measures were taken to future-proof the notebooks so that they can adapt to several situations such as ignoring blank lines and filtering names. 
        * If there are mistakes in the already existing structure, they can be easily fixed by editing the wiki page. 
        * If the structure changes, the notebook has been written so that it can be easily modified.
    * Data can be missing
        * For this dataset, blank spaces have been deliberately kept in. The statistics used can depend on the game and even the vehicle. 
        * For example:
            * In Forza Motorsport 1 and 2, most vehicles have a "Rarity Rating" (a float value), whereas in Forza Motorsport 7, Forza Horizon 4 and 5 and Forza Street, most vehicles have a "Rarity" (a string). 
            * In the Forza Horizon games, certain vehicles such as Traffic lack ratings statistics. 
            * Certain statistics for newly added vehicles for games still receiving new content might be temporarily absent until the values for the statistics in the game(s) are revealed in-game.
        * If a vehicle is not on the list, it will need to be added to the markup. 
        * If a statistic is not in a game, that row for each vehicle in the game will be blank.
        * When performing data visualisation, if a vehicle record for a game is missing a statistic that other records of that game should have, that record should be omitted. The number of omitted records should also be displayed in the visualisation. 
        * There are some statistics which do apear in the game but don't appear in the markup, such as vehicle "Division" or "Type" (e.g. Vintage Racers) for vehicles in Forza Horizon 4 and 5. 
            * This would require either adding the statistic to the vehicle list markup or going to each vehicle link and obtaining the statistic from the markup. The latter is a proposed further development, but for a start, I will only use the data available from the vehicle lists.
    * Data can be might not be regularly updated
        * The Forza Wiki is constantly updated to document new content being added to the latest games. 
        * Since people are contributing, the updating is not always instantaneous. 
        * Keep in mind the aforementioned newly added vehicles with missing statistic values. If the values are revealed in-game, the markup can be updated to include these values.
* The project has been provided with stable copies of the markup for each vehicle list. These are intended for testing purposes, but it also helps demonstrate the code functionality even if the page structure significantly changes.

## Proposed further development:
* Accessing pages of individual vehicles in order to extract further information not displayed in the vehicles list pages.
* Further handling of vehicle statistics updates to a saved dataset when accessing the pages via thg API (through a case-by-case basis, let the user choose which vehicles to update).
* Creating and hosting a full-stack web application, along with an API of the dataset. What is being considered for it includes:
    * Several cloud service tools (such as AWS Amplify or MongoDB Atlas).
        * The cloud service provider itself (such as AWS or Azure)
    * The choice of web frameworks/libraries (such as React, Svelte or Rocket).
    * GraphQL for declarative API data fetching.
* Creating more notebooks for other racing game series, such as:
    * Gran Turismo
    * Need For Speed
    * The Crew
    * Test Drive
    * Midnight Club
    * Dirt
    * Grid
    * WRC
    * Ride

## Project History
### evo1 - 25/08/23
* After previous experimentation with web-scraping via Selenium, I discovered and switched to using the MediaWiki API. This approach is easier and more reliable. It also allows the code to be easy to change and adapt if the pages get restructured.
* Implemented Pandas and Plotly.
* Used the vehicle list pages from the Forza wiki, which provides a good amount of data to perform data analysis and visualisation on without needing to access individual vehicle pages.

## References
* This project uses or has previously used material from the vehicle list pages for every released (as of commit) game in: 
    * the Forza series on the [Forza wiki](https://forza.fandom.com) at [Fandom](https://www.fandom.com/)
    * the Gran Turismo series on the [Gran Turismo wiki](https://gran-turismo.fandom.com) at [Fandom](https://www.fandom.com/)
* It is licensed under the [Creative Commons Attribution-Share Alike License (CC-BY-SA 3.0)](https://creativecommons.org/licenses/by-sa/3.0/).
* The API request code is based on:
    * https://www.jcchouinard.com/wikipedia-api/
    * https://community.fandom.com/f/p/3814380756008962153 