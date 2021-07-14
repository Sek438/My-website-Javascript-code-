// array for storing week days
var daysInWeek = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
// array for list of promotion 
var availablePromotions = ["", "Treatment", "", "", 
"Free Pedicure", "", "Eye lash fix", "", 
"", "", "Free Make-up", 
"Weaving", "", "", 
"", "Freebies", "", 
"", "", "", 
"", "", "", 
"", "", "", 
"", "", "", "", ""];

// array for when there is promotion
var hadPromotion = ["no", "yes", "no", "no", "yes", "no", 
"yes", "no", "no", "no", "yes", "yes", 
"no", "no", "no", "yes", "no", "no", "no", 
"no", "no", "no", "no", "no", "no", "no", 
"no", "no", "no", "no", "no"];

// function to place daysInWeeks values in header row cells 
function addMyDate() {
    var i = 0;
    while (i < 7) {
        document.getElementsByTagName("th")[i].innerHTML = daysInWeek[i];
        i++;
    }
}

// runs addColumnHeaders () function when page loads
window.addEventListener("load", addMyDate, false);

// function to place day of month value in first p element 
// within each table data cell that has an id

function addMonthDay() {
    var i = 1;
    var paragraphs = "";
    do {
        var tableCell = document.getElementById("08-" + i);
        paragraphs = tableCell.getElementsByTagName("p");
        paragraphs[0].innerHTML = i;
        i++;
    } while (i <= 31);
}

// function to populate calendar 
function setUpPage() {
    addMyDate();
    addMonthDay();
    addInfo();
}

// runs setUpPage() function when page loads
window.addEventListener("load", setUpPage, false);

// function to place opponent values in second p element within each table data cell that has an id 
function addInfo() {
    var paragraphs = "";
    for (var i = 0; i < 31; i++){
        var date = i + 1;
        var tableCell = document.getElementById("08-" + date);
        paragraphs = tableCell.getElementsByTagName("p");
        if (hadPromotion[i] === "yes"){
            paragraphs[1].innerHTML = "@ ";
        }
        if (hadPromotion[i] === "no") {
            paragraphs[1].innerHTML = "";
        }
        paragraphs[1].innerHTML += availablePromotions[i];
    }
}

// section to display the event details in the calenar text box 
function myMsg(){
    var mymessge = "Promotion: Treatment\rDate: 01-04-2020\rTime: 14:00PM\rVenue: Attraction Beauty Salon";
    document.getElementById("calendarDisplay").innerHTML = mymessge;
}

function myMsg2(){
    var mymessge = "Promotion: Free Pedicure\rDate: 05-04-2020\rTime: 14:00PM\rVenue: Attraction Beauty Salon";
    document.getElementById("calendarDisplay").innerHTML = mymessge;
}

function myMsg5(){
    var mymessge = "Promotion: Eye lash fix\rDate: 25-04-2020\rTime: 14:00PM\rVenue: Attraction Beauty Salon";
    document.getElementById("calendarDisplay").innerHTML = mymessge;
}

function myMsg3(){
    var mymessge = "Promotion: Free make-up\rDate: 16-04-2020\rTime: 14:00PM\rVenue: Attraction Beauty Salon";
    document.getElementById("calendarDisplay").innerHTML = mymessge;
}

function myMsg4(){
    var mymessge = "Promotion: Weaving\rDate: 23-04-2020\rTime: 12:00PM\rVenue: Attraction Beauty Salon";
    document.getElementById("calendarDisplay").innerHTML = mymessge;
}



PHOTO GALLERY JAVASCRIPT 
// use strict mode 
"use strict"; 
var autoMove = setInterval (moveImageRight, 5000);

/* photo arrangement aray */
var picArrangement = [1,2,3,4,5];

// number of pictures 
var figureCount = 3;


/* function to add pictures to the source */
function showFigures() {
    var nameOfFile;
    var currentFig;
    
    if (figureCount === 3){
    for (var i = 1; i < 4; i++){
        nameOfFile = "images/IMG_0" + picArrangement[i] + "sm.jpg";
        currentFig = document.getElementsByTagName("img")[i - 1];
        currentFig.src = nameOfFile;
    }
    
    } else {
        for (var i = 0; i < 5; i++){
            nameOfFile = "images/IMG_0" + picArrangement[i] + "sm.jpg";
            currentFig = document.getElementsByTagName("img")[i];
            currentFig.src = nameOfFile;
        }
    }
}

/* shift all images one figure to the left, and change values in picArrangement array to match  */
function moveImageRight() {
    //clearInterval(autoMove);
   for (var i = 0; i < 5; i++) {
      if ((picArrangement[i] + 1) === 6) {
         picArrangement[i] = 1;
      } else {
         picArrangement[i] += 1;
      }
      showFigures();
   }
}

/* shift all images one figure to the right, and change values in picArrangement array to match  */
function moveImageLeft() {
    clearInterval(autoMove);
   for (var i = 0; i < 5; i++) {
      if ((picArrangement[i] - 1) === 0) {
         picArrangement[i] = 5;
      } else {
         picArrangement[i] -= 1;
      }
      showFigures();
   }
}

/* switch image to 5 image layout */
function previewFive(){
    
    var articleEI = document.getElementsByTagName("article")[0];
    
    // create figure and img elements for fifth image
    var lastFigure = document.createElement("figure");
    lastFigure.id = "fig5";
    lastFigure.style.zIndex = "5";
    lastFigure.style.position = "absolute";
    lastFigure.style.right = "45px";
    lastFigure.style.top = "67px";
    
    var lastImage = document.createElement("img");
    lastImage.width = "240";
    lastImage.height = "135";
    
    lastFigure.appendChild(lastImage);
    //articleEI.appendChild(lastFigure);
    articleEI.insertBefore(lastFigure, document.getElementById("moveImageRight"));
    
    // clone figure element for fifth image and edit to be first image
    var firstFigure = lastFigure.cloneNode(true);
    firstFigure.id = "fig1";
    firstFigure.style.right = "";
    firstFigure.style.left = "45px";
    //articleEI.appendChild(firstFigure);
    articleEI.insertBefore(firstFigure, document.getElementById("fig2"));
    
    figureCount = 5;
    
    // add appropriate src values to two new img elements
    document.getElementsByTagName("img")[0].src = "images/IMG_0" + picArrangement[0] + "sm.jpg";
    document.getElementsByTagName("img")[4].src = "images/IMG_0" + picArrangement[4] + "sm.jpg";
    
    
    // change button to hide extra images
    var numberButton = document.querySelector("#fiveButton p");
    numberButton.innerHTML = "Show fewer images";
    if(numberButton.addEventListener){
        numberButton.removeEventListener("click", previewFive, false);
        numberButton.addEventListener("click", previewThree, false);
    } else if (numberButton.attachEvent){
        numberButton.detachEvent("onclick", previewFive);
        numberButton.attachEvent("onclick", previewThree);
    }
}

/* switches to three image layout */
function previewThree() {
    var articleEI = document.getElementsByTagName("article")[0];
    var numberButton = document.querySelector("#fiveButton p");
    
    articleEI.removeChild(document.getElementById("fig1"));
    articleEI.removeChild(document.getElementById("fig5"));
    
    figureCount = 3;
    numberButton.innerHTML = "Show more images";
    if(numberButton.addEventListener){
        numberButton.removeEventListener("click", previewThree, false);
        numberButton.addEventListener("click", previewFive, false);
    } else if (numberButton.attachEvent){
        numberButton.detachEvent("onclick", previewThree);
        numberButton.attachEvent("onclick", previewFive);
    }
}

/* Create event listeners for left arrow, right arrow and center figure element*/
function createEventListeners(){
    
    // for the left arrow 
    var moveImageLeft = document.getElementById("moveImageLeft");
    if (moveImageLeft.addEventListener){
        moveImageLeft.addEventListener("click", moveImageLeft, false);
    } else if (moveImageLeft.attachEvent){
        moveImageLeft.attachEvent("onclick", moveImageLeft);
    }
    
    // for the right arrow 
    var moveImageRight = document.getElementById("moveImageRight");
    if (moveImageRight.addEventListener){
        moveImageRight.addEventListener("click", moveImageRight, false);
    } else if(moveImageRight.attachEvent){
        moveImageRight.attachEvent("onclick", moveImageRight);
    }
    
    // to code to call a function when the user clicks the middle image to zoom
    var mainFig = document.getElementsByTagName("img")[1];
    if (mainFig.addEventListener){
        mainFig.addEventListener("click", zoomFig, false);
    } else if (mainFig.attachEvent){
        mainFig.attachEvent("onclick", zoomFig);
    }
    
    // event listener for the preview five button
    var showAllButton = document.querySelector("#fiveButton p");
    if (showAllButton.addEventListener) {
        showAllButton.addEventListener("click", previewFive, false);
    } else if (showAllButton.attachEvent){
        showAllButton.attachEvent("onclick", previewFive);
    }
}

/* open center figure in separate window */
function zoomFig() {
    var propertyWidth = 960;
    var propertyHeight = 600;
    var winLeft = ((screen.width - propertyWidth) / 2);
    var winTop = ((screen.height - propertyHeight) / 2);
    var winOptions = "width=960,height=600";
    winOptions += ",left" + winLeft;
    winOptions += ",top" + winTop;
    
   var zoomWindow = window.open("zoom.htm", "zoomwin", winOptions);
   zoomWindow.focus();
}

/* create event listeners and populate image elements */
function setUpPage() {
   createEventListeners();
   showFigures();
}

/* run setUpPage() function when page finishes loading */
if (window.addEventListener) {
  window.addEventListener("load", setUpPage, false); 
} else if (window.attachEvent)  {
  window.attachEvent("onload", setUpPage);
}


JAVASCRIPT TO ZOOM PICTURE


"use strict"; 
/* global variables */
var photoArrangement = window.opener.photoOrder;
var picName = "images/IMG_0" + photoArrangement[2] + ".jpg";

/* create event listener for close button */
function createEventListener(){
    var closeWindowdowDiv = document.getElementsByTagName("p")[0];
    if (closeWindowdowDiv.addEventListener){
        closeWindowdowDiv.addEventListener("click", closeWindow, false);
    } else if(closeWindowdowDiv.attachEvent){
        closeWindowdowDiv.attachEvent("onclick", closeWindow);
    }
}

/* close window*/
function closeWindow(){
    window.close();
}

/* populate img element and create event listener */
function pageSetup() {
   document.getElementsByTagName("img")[0].src = picName; // assign filename to img element
   createEventListener();
}

/* add img src value and create event listener when page finishes loading */
window.onload = pageSetup;

Page 2 – Create Promotion

JAVASCRIPT FOR DATE FIELD TO GENERATE DATE  
"use strict";
var newDate = new Date();

function displayCalendar(whichMonth){
    var date;
    var todaysDate = new Date();
    var dayOfWeek;
    var daysInMonth;
    var captionValue;
    var dateCells;
    var month;
    var year;
    var monthArray = ["January", "February", "March", "April", "May", "June", "July",
    "August", "September", "October", "November", "December"];
    
    if (whichMonth === -1){
        newDate.setMonth(newDate.getMonth() - 1);
    } else if (whichMonth === 1){
        newDate.setMonth(newDate.getMonth() + 1);
    }
    month = newDate.getMonth();
    year = newDate.getFullYear();
    newDate.setDate(1);
    dayOfWeek = newDate.getDay();
    captionValue = monthArray[month] + " " + year;
    document.querySelector("#cal table caption").innerHTML = captionValue;
    
if(month === 0 || month  === 2 || month === 4 || month === 6 || month === 7 || month === 9 || month ===11){
        daysInMonth = 31
    } else if(month === 1){ // Feb
        if(year % 4 === 0){ // leap year 
            if(year % 100 === 0){
                // year ending in 00 not a leap year unless divisible by 400
                if(year % 400 === 0){
                    daysInMonth = 29
                } else {
                    daysInMonth = 28;
                }
            } else {
                daysInMonth = 29;
            }
        }else {
            daysInMonth = 28;
        }
    } else {
        daysInMonth = 30;
    }
    
    dateCells = document.getElementsByTagName("td");
for (var i = 0; i < dateCells.length; i++){
    dateCells[i].innerHTML = "";
    dateCells[i].className = "";
}

for (var i = dayOfWeek; i < daysInMonth + dayOfWeek; i++){
    dateCells[i].innerHTML = newDate.getDate();
    dateCells[i].className = "date";
    if(todaysDate < newDate){
        dateCells[i].className = "futuredate";
    }
    date = newDate.getDate() + 1;
    newDate.setDate(date);
}
    newDate.setMonth(newDate.getMonth() - 1);
    // reset month to month shown
    document.getElementById("cal").style.display = "block";
    // display calendar if it's not already visible
}

// code to select a date from the calendar
function selectPreferredDate(event){
    if(event === undefined) { // get caller element in IE8
        event = window.event;
    }
    var callerElement = event.target || event.srcElement;
    
    if(callerElement.innerHTML === ""){
        // cell contains no data, so don't close the calendar 
        document.getElementById("cal").style.display = "block";
        return false;
    }
    newDate.setDate(callerElement.innerHTML);
    
    var fulltodaysDate = new Date();
    var todaysDate = Date.UTC(fulltodaysDate.getFullYear(), fulltodaysDate.getMonth(), fulltodaysDate.getDate());
    var selectedDate = Date.UTC(newDate.getFullYear(), newDate.getMonth(), newDate.getDate());
    if (selectedDate <= todaysDate){
        document.getElementById("cal").style.display = "block";
        return false;
    }
    document.getElementById("promotionDate").value = newDate.toLocaleDateString();
    
    hideCalendar();
}

// function hide the calendar 
function hideCalendar(){
    document.getElementById("cal").style.display = "none";
}

// function to display the previous
function movePreviousMonth(){
    displayCalendar(-1);
}

// function to display the next month
function moveNextMonth(){
    displayCalendar(1);
}

// function to create eventListener
function createEventListeners(){
    var dateField = document.getElementById("promotionDate");
    if (dateField.addEventListener){
        dateField.addEventListener("click", displayCalendar, false);
    } else if(dateField.attachEvent){
        dateField.attachEvent("onclick", displayCalendar);
    }
    
    var dateCells = document.getElementsByTagName("td");
    if (dateCells[0].addEventListener){
        for(var i = 0; i < dateCells.length; i++){
            dateCells[i].addEventListener("click", selectPreferredDate, false);
        }
    }
    
    
    var closeButton = document.getElementById("close");
    if(closeButton.addEventListener){
        closeButton.addEventListener("click", hideCalendar, false);
    } else if(closeButton.attachEvent){
        closeButton.attachEvent("onclick", hideCalendar);
    }
    
    
    var prevLink = document.getElementById("prev");
    var nextLink = document.getElementById("next");
    if(prevLink.addEventListener){
        prevLink.addEventListener("click", movePreviousMonth, false);
        nextLink.addEventListener("click", moveNextMonth, false);
    }else if(prevLink.attachEvent){
        prevLink.attachEvent("onclick", movePreviousMonth);
        nextLink.attachEvent("onclick", moveNextMonth);
    }
}

if (window.addEventListener){
    window.addEventListener("load", createEventListeners, false);
} else if(window.attachEvent){
    window.attachEvent("onload", createEventListeners);
} else if(dateCells[0].attachEvent){
    for(var i = 0; i < dateCells.length; i++){
        dateCells[i].attachEvent("onclick", selectPreferredDate);
    }
}
