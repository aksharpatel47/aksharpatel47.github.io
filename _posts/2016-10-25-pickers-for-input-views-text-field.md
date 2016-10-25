---
layout: post
title: Pickers as Input views for Text Fields
categories: tutorial,swift,ios
date: 2016-10-25
tags: UITextField,UIDatePicker,inputView,accessoryView
---

The most common UI interactions we do, in our mobile apps, is entering data into the app. If we want
to limit the user to a particular set or type of values, we can allow the user to pick those values
from pickers when the user tries to enter data in a text field. The way we do this is by configuring
UIPickerView / UIDatePicker to be inputViews of UITextField. We'll explore this idea further in 
this blogpost.

### Getting Started

For this project, we'll use Swift 3.0 and Xcode 8. Create a new Single Page iOS app with Swift 3 
as its language in Xcode. Open the Main.storyboard and add a text field to the view controller. 
Make the text field centered and add missing contraints.

![Initial View of the Controller](/assets/images/date_picker_text_field_initial_view.jpeg)

Link this textfield to ViewController.swift. Below is our initial ViewController.swift.

{% highlight swift %}

class ViewController: UIViewController {
  // MARK: Properties
  var datePicker: UIDatePicker!
  var inputAccessoryBar: UIToolbar!

  // MARK: Outlets
  @IBOutlet weak var textField: UITextField!

  // MARK: Lifecycle Methods
  override func viewDidLoad() {
    //TODO: To implement
  }
}
{% endhighlight %}

### Date Picker as InputView

Let's start by creating a function that initializes a UIDatePicker. This date picker will be
used to select values for the text field.

{% highlight swift %}
func initializeDatePicker() {
  datePicker = UIDatePicker()
  datePicker.datePickerMode = .date
  datePicker.date = Date()
  datePicker.addTarget(self, action: #selector(onDateChanged), for: .valueChanged)
}
{% endhighlight %}

We'll need two helper functions here. One which changes the value of the text field based on
the value of date picker. The other takes the date value of the date picker and formats it into 
readable date string.

{% highlight swift %}
func onDateChanged(sender: UIDatePicker) {
  textField.text = getDateString(from: sender.date);
}

func getDateString(from date: Date) -> String {
  let dateFormatter = DateFormatter()
  dateFormatter.dateStyle = .medium
  return dateFormatter.string(from: date)
}
{% endhighlight %}

We now have the date picker set up. Now, we just need to add it to our text field's input view.

{% highlight swift %}
override func viewDidLoad() {
  initializeDatePicker()
  textField.inputView = datePicker
}
{% endhighlight %}

Let's have a look at the output...

![UIDatePicker as inputView of UITextField](/assets/images/date_picker_text_field_input_view.jpeg)

We have successfully added a picker as an input view to the text field. But, something's still lacking. The user
has no way of dismissing the picker. As we're using a picker instead of a keyboard for input, we'll need to
give our user a way to dismiss the picker. For this, we add an accessory toolbar bar above our picker with a done
button. Clicking on this done button dismisses the picker.

Let's write one function which creates an accessory bar and another function which dismisses the date picker.

{% highlight swift %}
func initializeInputAccessoryBar() -> UIToolBar {
  toolBar = UIToolbar(frame: CGRect(x: 0, y:0, width: view.frame.width, height: 44))
  let doneButton = UIBarButtonItem(title: "Done", style: .done, target: self, action: #selector(dismissDatePicker))
  let flexibleSpace = UIBarButtonItem(barButtonSystemItem: .flexibleSpace, target: self, action: nil)
  toolBar.items = [flexibleSpace, doneButton]
}

func dismissDatePicker() {
  textField.resignFirstResponder()
  textField.text = getDateString(from: datePicker.date)
}
{% endhighlight %}

Having created an accessory toolbar, let's add the the toolbar to be an input accessory view for the textField

{% highlight swift %}
override func viewDidLoad() {
  // Create and add date picker to textField's input view
  initializeDatePicker()
  initializeInputAccessoryBar()

  textField.inputView = datePicker
  textField.inputAccessoryView = inputAccessoryBar
}
{% endhighlight %}

### End Result

Let's look at what we've built.

![UIDatePicker and UIToolBar helping us make UITextField easy to use for picking data](/assets/images/date_picker_input_field_final.jpeg)

That's it. We've successfully implemented date pickers to be inputView for our textField. We can even implement UIPickerView to be
the inputView in the same way. I'll leave this as an exercise for the readers to explore.