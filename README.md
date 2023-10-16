Tests overlays using Jetpack Compose

I used Sam Edwards work to create the initial scaffolding to solve the problem
of the missing lifecycle owner and saved state registry owner (my initial
attemps where too naive).

https://www.jetpackcompose.app/snippets/OverlayService

I had to update a few things to make it compile and work with current Jetpack
libraries.

Also, more importantly, the lifecycle was moved to CREATE, but it was not
STARTed nor RESUMEd. Without that, recomposition was not happening.

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
