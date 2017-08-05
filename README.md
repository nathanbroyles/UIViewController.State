# UIViewController.State

UIViewController.State is a... stateful approach to updating user interfaces. 

## var state: State = .new

The key to this approach is the state variable. It will be used throughout the view controller when something takes place that requires the UI to update. 
`var state: State`

I’m going to define my `State` enum now.  
```
class MyViewController: NSViewController {

    var state: State = .new

    enum State {
        case new
        case done
    }
    ...
```

## Updating state
In `viewDidLoad` I’m going to set my initial state. 
```
override func viewDidLoad() {
    super.viewDidLoad()

    state = ViewController.State.new
}
```

I have a button that submits a form and needs to update the UI to display a done message.
```
@IBAction func thingPressed(_ sender: NSButton) {
    // do stuff

    // update state
    state = MyViewController.State.done
}
```
Awesome. That is super easy for me to understand what is going on.  

Next I need to do something after `state` gets updated. I’m going to add a `didSet` to my `state` property and a `switch` statement.  
```
var state: State = .new {
    didSet {
        switch state {
        case .new:
            formStackView.isHidden = false
            doneView.isHidden = true
        case .done:
            formStackView.isHidden = true
            doneView.isHidden = false
        }
    }
}
```
Rad. Now I have all of my UI updating code all in one neat place.

If I want to reset my view, all I need to do is set the `state` property again.  
```
@IBAction func doItAgainPressed(_ sender: Any) {
    // update state
    state = MyViewController.State.new
}
```
My `didSet` will run and my view will be reset.

😎
