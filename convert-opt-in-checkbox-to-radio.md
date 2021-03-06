This is useful if you wish to test out radio opt-ins versus the traditional checkbox opt-ins.

The code, when placed on your page in a code block, will transform the checkbox into a radio.

**Note:** you need to test that your data is still stored as expected. This code is not part of the normal operations of the platform.

To implement:

1) Create your page as normal
2) Get the field name and ID of the checkbox - the method is:
    1) Preview the page
    2) Right-click and choose "Inspect" or "Inspect Element"
    3) In the window that appears, click the arrow icon and click on your checkbox opt-in. The HTML for it should show
    4) View the HTML to find the element name and ID. For example, in the image below you can see that the last class listed in the topmost div of the opt-in is ```en__fieldcat-opt-in``` and the ID is ```19328``` . Yours will differ
3) Edit the page and add a new code block below the checkbox. Clear the contents and amend the ```optInField``` and ```optInInputID``` so they are the same values as you discovered 
4) View and test

**How to find the IDs of your opt-in**
![How to find the variables](https://github.com/EngagingNetworks/page-builder-code-blocks/blob/master/convert-checkbox-to-radio.png?raw=true)

**Code block**
``` html
<script>
    // This script takes a checkbox opt-in and converts it to a radio opt-in
    // This can be useful for testing how supporters react to opt-in type
    // Please test this thoroughly
    
    // Checkbox to convert
    var optInField = "en__field--cat-opt-in"; // CHANGE THIS VALUE
    var optInInputID = "19328"; // CHANGE THIS VALUE
    // Labels of new radio
    var radioYesLabel = "Yes";
    var radioNoLabel = "No";
    // Convert checkbox
    $("." + optInField).removeClass("en__field--checkbox").addClass("en__field--radio");
    $("." + optInField + " .en__field__element").removeClass("en__field__element--checkbox").addClass("en__field__element--radio");
    $("." + optInField + " input").removeClass("en__field--checkbox").addClass("en__field--radio");
    $("." + optInField + " input").attr("type","radio");
    $("." + optInField + " input").removeClass("en__field__input--checkbox").addClass("en__field__input--radio");
    $("." + optInField + " .en__field__item label").text(radioYesLabel);
    // Additional radio button html
    var newRadio = "<div class='en__field__item'><input id='en__field_supporter_questions_" +
        optInInputID + "Y' type='radio' class='en__field__input en__field__input--radio' value='N' name='supporter.questions." +
        optInInputID + "'><label for='en__field_supporter_questions_" +
        optInInputID + "Y' class='en__field__label en__field__label--item'>" + radioNoLabel + "</label></div>"
    // Add additional radio
    $("." + optInField + " .en__field__item").after ( $(newRadio) );
</script>
```
