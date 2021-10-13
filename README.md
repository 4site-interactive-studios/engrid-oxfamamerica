
# engrid-oxfamamerica
ENgrid Oxfam America Custom Code for In Memory Ecards

### Donation Page (Page 1)

1: Add "In Memoriam" field to Form Block

2: Add "Honoree Name" and "Tribute Type Suppporter Field" to second Form Block with a CSS Class of `inmem-Y`

3: Add the following CSS

    <style>
    #engrid .en__field--inmem label.en__field__label.en__field__label--item{
        font-family: Roboto-Regular-webfont,Arial,sans-serif;
        color: #545454;
        box-sizing: border-box;
        padding: 0;
        position: relative;
        margin-left: 2rem;
        cursor: pointer;
        align-items: center;
        vertical-align: top;
        width: auto;
        font-size: 2rem;
        font-weight: 400;
        text-transform: none;
        letter-spacing: .4px;
        display: inline-block;
        line-height: 1.4;
        border: 0;
        background: transparent;
    }
    #engrid .en__field--inmem label.en__field__label.en__field__label--item:before{
        content: "" !important;
        position: absolute;
        height: 1.4rem;
        width: 1.4rem;
        left: -2rem;
        display: inline-block !important;
        vertical-align: middle;
        border: 2px solid var(--client-black,#545454);
        background-color: var(--client-white,#fff);
        cursor: pointer;
        transition-duration: .25s;
        transition-property: border-color,background-color;
        border-radius: 0;
        box-shadow: none;
        top: 7px;
    }
    </style>

### Donation Page (Page 2)

1: Add the "Click here to send your eCard" link

    <div class="send-if-ecard"><a class="pseduo__en__submit_button" href="https://act.oxfamamerica.org/page/34382/action/1?chain">Click here to send your eCard</a></div>

2:  Add in these styles

    <style>
    .send-if-ecard a{
        transition: background-color .25s ease-out,color .25s ease-out;
        text-align: center;
        background-color: var(--client-submit-button-background-color,#f16e22);
        border-color: var(--client-submit-button-background-color,#f16e22);
        color: #FFF !important;
        text-decoration: none;
        border-radius: var(--client-button-border-radius,5px);
        display: block;
        line-height: 1;
        font-size: 2rem;
        font-family: oxfam_tstar_proheadline,RobotoCondensed-Bold-webfont,Arial,sans-serif;
        font-weight: 400;
        min-width: 250px;
        width: auto;
        margin: 20px auto;
        padding: 1em 3em;
        max-width: 450px;
    }
    .send-if-ecard a:hover{
        background-color: var(--client-submit-button-background-color-hover,#bb4c0c);
    }
    </style>

3: Add in this script
   
     <script>
     window.addEventListener('DOMContentLoaded', function() {
         // Hide eCard Button if eCard field was not checked
         if(!localStorage.getObj("supporter.NOT_TAGGED_91")){
             const sendIfEcard = document.querySelector(".send-if-ecard");
             if(sendIfEcard) sendIfEcard.style.display = "none";
         }
     });
      </script>

### ECard Page (Page 1)

1: Add these styles

    <style>
    .en__submit{
        margin: 20px auto;
    }
    .en__component--ecardblock .en__ecardrecipients__email input, .en__component--ecardblock .en__ecardrecipients__name input {
        width: 100%;
    }
    .en__component--ecardblock .en__ecardrecipients__email input{
        padding-right: 40px;
    }
    .en__ecarditems__addrecipient{
        bottom: 5px;
        right: 5px;
    }
    .en__ecarditems__list{
        display: flex;
        align-items: center;
        flex-wrap: wrap;
        justify-content: center;
        margin: 20px 0;
    }
    .en__ecarditems__thumb{
        margin: 0;
    }
    .en__ecardrecipients__recipient{
        flex-wrap: nowrap;
    }
    .en__ecardrecipients__recipient .ecardrecipient__email, .en__ecardrecipients__recipient .ecardrecipient__name{
        height: auto;
        border: var(--client-input-border-width,2px) solid var(--client-input-border-color,#cacaca);
        border-radius: var(--client-input-border-radius,5px);
        background-color: var(--client-input-background-color,#fff);
        box-shadow: inset 0 1px 2px rgba(10,10,10,.1);
        font-family: inherit;
        font-weight: 400;
        line-height: 1.5;
        color: var(--client-black,#545454);
        transition: box-shadow .25s,border-color .25s ease-in-out;
        appearance: none;
        font-size: 1.8rem;
        padding: 6px 10px;
        margin: 0 32px 0 0;
        width: 100%;
        min-height: 50px;
    }
    .en__ecardrecipients__recipient .ecardrecipient__remove {
        position: relative;
    }
    .en__ecardrecipients__recipient .ecardrecipient__remove button{
        transition: background-color .25s ease-out,color .25s ease-out;
        text-align: center;
        appearance: button;
        cursor: pointer;
        color: #fff;
        background: #ff4351;
        border: 0;
        border-radius: 4px;
        display: inline-block;
        position: absolute;
        font-weight: 700;
        width: 32px;
        height: 32px;
        font-size: 20px!important;
        padding: 0!important;
        font-family: arial!important;
        bottom: 5px;
        right: 5px;
        margin: 4px!important;
    }
    button.en__ecarditems__prevclose {
        align-items: center;
        border: none;
        display: flex;
        font-size: 2rem;
        height: auto;
        justify-content: center;
        margin: 0;
        padding: .35ch;
        right: 0;
        top: 0;
        width: auto;
    }
    </style>

2: Add in this script

    <script>
        // Only run on e-cards
    if (
      window.hasOwnProperty("pageJson") &&
      pageJson.hasOwnProperty("pageType") &&
      pageJson.pageType === "e-card"
    ) {
      // Get the form elements
      const formElements = document.querySelectorAll(
        "input[type='text'], textarea"
      );
      // Get Search Parameters
      const searchParams = new URLSearchParams(window.location.search);
      searchParams.forEach(function (value, key) {
        formElements.forEach(function (element) {
          element.value = element.value.replace(`{${key}}`, value);
        });
      });
    
      const pageDataUrl =
        location.protocol + "//" + location.host + location.pathname + "/pagedata";
      fetch(pageDataUrl)
        .then(function (response) {
          return response.json();
        })
        .then(function (json) {
          // Loop through the json object
          for (const key in json) {
            if (json.hasOwnProperty(key) && json[key] !== null) {
              console.log(key, json[key]);
              // Replace the form element with the json data
              formElements.forEach(function (element) {
                element.value = element.value.replace(`{${key}}`, json[key]);
              });
            } else {
              // Clear the form element
              formElements.forEach(function (element) {
                element.value = element.value.replace(`{${key}}`, "");
              });
            }
          }
        })
        .catch((error) => {
          console.error("PageData Error:", error);
        });
        // Auto-Click on Add Recipient Button if the end user forgets
        function checkRecipientFields() {
        const addRecipientButton = document.querySelector(
          ".en__ecarditems__addrecipient"
        );
        // If we find the "+" button and there's no hidden recipient field, click on the button
        if (
          addRecipientButton &&
          !document.querySelector(".ecardrecipient__email")
        ) {
          addRecipientButton.click();
        }
        return true;
      }
      window.enOnValidate = function(){
          return checkRecipientFields(); // validation was ok so return true
      }
    }
    </script>
