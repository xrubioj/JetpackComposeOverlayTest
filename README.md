# Tests overlays using Jetpack Compose

This is a small test project to explore how to use Jetpack Compose in an
overlay.

## The problem

The main problem is that there are a few requirements that are
usually implemented in the `Activity` that are not available when you simply
instantiate a `ComposeView‎` to wrap you Compose code. 

I used Sam Edwards work to create the initial scaffolding to solve the problem
of the missing lifecycle owner and saved state registry owner (my initial
attemps where too naive).

https://www.jetpackcompose.app/snippets/OverlayService

I had to update a few things to make it compile and work with current Jetpack
libraries, as Sam's example was for an older version.

Also, more importantly, the lifecycle was transitioned to CREATE, but it was
not STARTed nor RESUMEd. Without that, recomposition was not happening.

## Code structure

- `com.xrubio.overlaytest.MainActivity` has code to request overlay permission and to start the overlay (currently the only way to remove it is to remove the permission or fully stop the app).
- `com.xrubio.overlaytest.overlay` package contains the example code.
- `AndroidManifest.xml` contains the permissions to show the overlay and to show notifications (used to show a `Toast` from the overlay code when the app is in the background).

## Other considerations

Also, notice that in order for the app to work it requires the user to enable
overlays (if you tap the "Open Overlay Activity" button it opens the system
settings) and also needs the user to manually enable notifications for the
app (the permission is there, but I haven't implemented the code to request
it yet).

Finally, currently there's no way to dismiss the overlay. This is just a
small PoC. I may implement it later.

UPDATE: the original Gist with comments pointing out to the same solutions
I found seems to be here:

https://gist.github.com/handstandsam/6ecff2f39da72c0b38c07aa80bbb5a2f
