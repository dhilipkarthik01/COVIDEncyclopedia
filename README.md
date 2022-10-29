# COVIDEncyclopedia
# Description
- An Android application written with a mix of Java and Kotlin which gives all information on the COVID19 pandemic.
- It provides information about the virus, it can also show the whole of India on a map and how affected a certain place is.
- The app is also able to predict the impact of the virus on a near future date and can also find the nearest vaccination centers on a selected 
date using your location
- Overall the app intends to make people more aware of latest news on the virus.

# How to run on your computer
Ensure you have Android Studio downloaded and set up with an Emulator (AVD) to run the project

1. Copy the repository link from Github under the Code section
2. Open Android Studio Click on File -> New -> Project from Version Control
3. Paste the copied repository link on the URL field and verify the path in which your project files will be stored and created then click Clone
4. After cloning check the path you specified to see the project folder
5. Click on the play button to run the app (May take some time)
6. The app runs successfully on the emulator

Setting up Virtual Device (AVD) in Android Studio | Android Emulator

Link: https://www.youtube.com/watch?v=x_lvdLil0Fk

Running this project on your computer demo : https://youtu.be/7ZJ0uH-1T_g

You can also download the .apk file from https://drive.google.com/file/d/1watXfOslvewLPFRqGmCLHzPG9DdVMsnC/view?usp=sharing to run the app

# Features of COVID Encyclopedia
- Display of confirmed, recovered and deceased patients across all states of India
- Choropleth map visualization of the impact of COVID across India which gives an idea of the COVID hotspots of India
- Display of risk (both a quantitative estimate and qualitative) of COVID for touring across India (district-wise).
- Forecasting the risk for touring in the near future using Holt-Winters exponential smoothing (India district-wise).
- Display of the nearest vaccination centers using your location on the selected date
- Displays various details like Hospital name, working hours, address, type of vaccine, age limit, availability etc

# Concepts used in COVID Encyclopedia
- During opening of the app we have a Splash Screen displayed for 3 seconds
- The home screen and other transitional pages use CardView arranged below each other.
- Clicking leads us to the desired activity.
- We have 4 main modules
1. COVID19 Tracker
2. COVID19 Hotspots
3. Touring risk prediction
4. Nearest Vaccine centrt

# COVID19 Tracker
- UI created with a TextView, RecyclerView, StateAdapter and ArrayList, List with a custom defined model
- API Link : https://api.rootnet.in/covid19-in/stats/latest
- API contains confirmed, recovered and deceased COVID cases for all states of India
- Fetching data from API as JSON objects using Volley library
- Format of how data for each state is defined using a custom model called Statemodel
- All Statemodels are appended onto a List (StateList)
- Use of Adapter (StateAdapter) for displaying a RecyclerView item based on loading state.
- Linear layout to show the list of states one below the other

# COVID19 Hotspots
- Extracting total confirmed cases for each state from https://data.covid19india.org/csv/latest/districts.csv
- Assigning a relative impact for each state considering the relative impact on other states.
- Using plotly express to plot an interactive choropleth map of the impact of each state.
- Clicking on each state on the map gives the impact and total cases in that state
- Extracting the choropleth map as a html file from plotly express and storing as an Asset in Android
- Using a WebView to display the map in html format onto an activity.

# Touring risk prediction
- Using data from https://data.covid19india.org/csv/latest/districts.csv which is time series district-wise data
- Using Holt-Winters trend forecasting algorithm to forecast the risk of COVID on a specific district in the near future using script from https://github.com/mrsurya1304/COVID19-Impact-Prediction/blob/main/COVID-19_Touring_Risk_Prediction.ipynb
- Getting the results of the model from the script for all states for a forecast of 3 months and converting it to JSON format
- Hosting the data onto a Heroku app for use in COVID Encyclopedia https://covidencyclopedia1.herokuapp.com/?a=" + i1 + "&b=" + i2
- UI created with a TextView and a DatePickerDialog with a set range for the data we have
- Fetching data from Heroku as JSON objects using Volley library
- Showing data as alert boxes of different color according to the risk obtained
- Text from the alert box also has audio obtained from TexttoSpeech with english as the set language

# Nearest Vaccine center
- UI created with a TextView, Buttons, RecyclerView, RecyclerView Model, Adapter and  List with a custom defined model
- Use of LocationManager and Geolocator to get device locattion and to extract pincode.
- DatePicker dialog for user to select date
- API Link: https://cdn-api.co-vin.in/api/v2/appointment/sessions/public/calendarByPin?pincode="+pinCode+"&date="+date
- Given pincode and date the API can gather the vaccination centers in that pincode and extract details on each vaccination center including
Hospital name, working hours, address, type of vaccine, age limit, availability etc
- Fetching data from API as JSON objects using Volley library
- Format of how data for each vaccination center is placed and shown using a custom model called CenterModel
- Each CenterModel is added onto a List (centerList)
- Use of Adapter (CenterAdapter) for displaying a RecyclerView item based on loading state.
- Linear layout to show the list of vaccination centers one below the other


# How the app looks like
![alt text](https://github.com/mrsurya1304/COVIDEncyclopedia/blob/master/samples/sample1.png)
![alt text](https://github.com/mrsurya1304/COVIDEncyclopedia/blob/master/samples/sample2.png)
![alt text](https://github.com/mrsurya1304/COVIDEncyclopedia/blob/master/samples/sample3.png)
![alt text](https://github.com/mrsurya1304/COVIDEncyclopedia/blob/master/samples/sample4.png)
![alt text](https://github.com/mrsurya1304/COVIDEncyclopedia/blob/master/samples/sample5.png)

# Demo
Link: https://youtu.be/ZysWGw3pnLQ

# Future Ideas
- Bringing in detection of COVID positive patients nearby using Bluetooth
- Social distancing warning by detecting distance
- Symptoms warning, collection and detection of COVID of user and suggesting precautions and medication
- Display lockdown rules, mask mandates and other precausion in the location of the user

# Acknowledgements
Some ideas have been taken from GeeksforGeeks who have excellent videos on COVID19 Tracking and vaccine center finding

Covid-19 Tracker : https://www.youtube.com/watch?v=opCW91zYJcI

Covid-19 Vaccine Availability app: https://www.youtube.com/watch?v=F-E6mFPIOrY

Other ideas including Touring risk prediction and COVID hotspots visualization are from my team


