# Animations 
## Essential animation concepts and classes
* `Animation` interpolates the values used to guide an animation
* An `Animation` object knows the current state of an animation, but doesn't know anything about what appears onscreen.
* An `AnimationController` manages the `Animation`.
* A `CurvedAnimation` defines progression as a non-linear curve.
* A `Tween` interpolates between the range of data as used by the object being animated. 
* Use Listeners and StatusListeners to monitor animation state changes.

## `Animation<double>`
An `Animation` object sequentially generates interpolated numbers between two values over a certain duration. The output of an `Animation` object might be linear, a curve, a step function, or any other mapping you can devise. Depending on how the `Animation` object is controlled, it could run in reverse, or even switch directions in the middle.

An `Animation` object has state. Its current value is always available in the `.value` member.

An `Animation` object knows nothing about rendering or `build()` functions.

## Animation Controller
`AnimationController` is a special `Animation` object that generates a new value whenever the hardware is ready for a new frame. By default, an `AnimationController` linearly produces the numbers from 0.0 to 1.0 during a given duration. For example, the following code creates an `Animation` object, but does not start it: 

``` dart
controller = AnimationController(duration: const Duration(seconds: 2), vsync: this);
```
`AnimationController` derives from `Animation<double>`, so it can be used whenever an `Animation` object is needed. However, the `AnimationController` has additional methods to control the animation. For example, you start and animation with the `.forward()` method. The generation of numbers is tied to the screen refresh, so typically 60 numbers are generated per second. After each number is generated, each Animation object calls the attached Listener objects. To create a custom display list for each child, see `RepaintBoundary`. 

When creating an `AnimationController`, you can pass it a `vsync` argument. The presence of `vsync` prevents offscreen animations from consuming unnecessary resources. You can use your stateful object as the vsync by adding `SincleTickerProviderStateMixin` to the class definition. You can see an example of this in `animate1` on GitHub.

## Tween
By default, the `AnimationController` object ranges from 0.0 to 1.0. If you need a different range or a different data type, you can use `Tween` to configure an animation to interpolate to a different range or data type. For example, the following `Tween` ranges from -200.0 to 0.0:

``` dart
tween = Tween<double>(begin: -200, end: 0);
```

A `Tween` object does not store any state. Instead, it provides the `evaluate(Animation<double> animation)` method that applies the mapping function to the current value of the animation. 

### Tween.animate
To use a `Tween` object, call `anmiate()` on the `Tween`, passing the controller object. For example, the following generates the integer value from 0 to 255 over the course of 500ms.

``` dart
AnimationController controller = AnimationController
(
	duration: const Duration(milliseconds: 500), vsync: this
);
Animation<int> alpha = IntTween(begin: 0, end: 255).animate(controller);
```

## Animation Notifications
An `Animation` object can have `Listeners` and `StatusListeners`, defined with `addListener()` and `addStatusListener()`. A `Listener` is called whenever the value of the animation changes. The most common behavior of a `Listener` is to call `setState()` to cause a rebuild. 

# Animation Examples
To render with an `Animation` store the `Animation` object as a member of your widget, then use its value to decide how to draw.
