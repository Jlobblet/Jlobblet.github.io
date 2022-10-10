---
layout: post
title: "On Equivalence in Photography"
---

Within photography, the term "equivalent" or "equivalence" appears a lot, especially if you use a crop sensor.
I shoot using an Olympus E-M1 Mark III mostly, which has a Micro Four Thirds (MFT) sensor.
As a result, almost every lens I read about mentions a full frame (FF) "equivalent" focal length.
However, I don't especially like the term, for reasons I will get into in this article.

Depth of Field
--------------

Depth of field is a measure of the width of the region of the photograph that is sharp, along the axis perpendicular to the plane of the sensor (or through the lens).
A shallow depth of field is characterised by out-of-focus regions in front of and behind the subject, blurring the surrounding.
A deep depth of field is characterised by more of the photo being in focus.

The depth of field is given by an equation with a bunch of terms:

$$
\Delta = \frac{2u^2Nc}{f^2} \\
\intertext{where}
u \text{ is the distance to the subject}, \\
N \text{ is the f-number, given by} N = \frac{f}{D}, \\
c \text{ is the circle of confusion}, \\
f \text{ is the focal length, and} \\
D \text{ is the diameter of the entranct pupil.}
\intertext{Or equivalently,}
\begin{aligned}
\Delta  = \frac{2u^2Nc}{f^2} \\
\Delta &= \frac{2u^2 \frac{f}{D} c}{f^2} \\
\Delta &= \frac{2u^2c}{fD}
\end{aligned}
$$

This is where "equivalence" starts to creep in.
Sensor size has no _direct_ impact on depth of field.
So why do FF cameras have a shallower depth of field than MFT?

The answer is the focal length of the lenses[^coc].
An "equivalent" lens in MFT has a focal length half that of a FF lens.
For a concrete example, a 50mm FF lens is "equivalent" to 25mm in MFT terms.

Here, "equivalent" means equivalent angle of view.
The angle of view (sometimes called field of view) is the horizontal angle that the lens sees at.
Because of the crop factor of a MFT sensor (half the size of a FF sensor — crop factor is 2), half the focal length results in the same angle of view.
Other characteristics are not the same, most notably depth of field.

Given a MFT and FF lens with equivalent angle of view shooting at the same f-number, the FF will result in a shallower depth of field, owing to its longer focal length.
If the MFT lens needed to have the same depth of field as the FF, using the equation above, it would have to have half the f-number.

Equivalent Light-Gathering
--------------------------

Something that gets said a lot is that FF cameras perform better than cropped sensors in low-light conditions.
There's usually one of several reasons attached, but some of these make no sense.

Total Light
===========

The worst offender is the "because a FF sensor is bigger, it gathers more light".
The sensor doesn't gather any light at all — the lens does.

To consider this argument, let us consider two lenses: one for FF, one for MFT.
The lenses have the same aperture (and so, f-number), but the MFT lens has half the focal length of the FF, giving them the same angle of view.

Using the f-number equation $ N = \frac{f}{D} $, we can work out that the size of the entrance pupil is given by $ D = \frac{f}{N} $.
In other words, the entrance pupil is the focal length divided by the f-number.
The f-numbers of our lenses are identical, but the FF lens has twice the focal length — so the diameter of the entrance pupil is twice as big.
This means the area of the entrance pupil is four times larger, and the FF lens lets in four times as much light as the MFT lens.

However, the FF _sensor_ is also bigger.
In fact, its area is four times bigger than the MFT sensor's — the crop factor squared.
So the four times as much light it gathers has to be spread over a four times greater area, resulting in the same flux at the sensor.

Both lenses in this scenario collect as much light _per unit area_ of the sensor.
The FF does collect more _total_ light, but that doesn't matter.

However, the depth of field of the FF will be half that of the MFT, for reasons set out above.
The FF lens is still longer.
This may or may not be desirable; that is down to the artistic vision of the photographer or videographer.
If they want a deep depth of field in low-light conditions, a cropped sensor is superior because it collects the same light while providing that deeper depth of field.
A FF camera would have to stop down its lens to reach the same effect, reducing the amount of light reaching the sensor — typically undesirable in when shooting in low light.

I don't know why this particular assertion is so wide-spread.
Thinking about the logic involved for a few seconds should make it clear that even if the total light gathered is greater, the flux is the same.
I think it is likely based on observational results and a poor understanding of what causes them.

Pixel Size
==========

The reasoning here is "because FF sensors have biggers pixels, and so they are less noisy" or similar.
At this point we have to acknowledge a difference between the idealised case and the real world.
Camera sensors are made of pixels, which (in short) count the number of photons[^wpd] that hit them.

Larger pixels are better at gathering light, assuming you compare two sensors of the same size.
The impact this will have on the overall noise of the image in hard to determine and not generally clear.
But when sensors are different sizes, does this still hold?

As always, it depends on the shooting settings.
If the flux is the same, the larger pixels will perform better.
If the flux is different, the greater flux will eventually have the advantage over sensor size.

For an example where the flux would be different, consider having a specific _depth of field_ instead of aperture.
A MFT camera would have half the f-number of a FF one to get the same depth of field.
This would result in a greater flux at the sensor, so even with smaller pixels (which is typical for MFT compared to FF) it would result in a greater image quality.

However, in low-light conditions you usually shoot wide open to maximise the amount of light entering the camera.
Here, FF cameras do have an advantage assuming shallow depth of field is desirable.
If a deep depth of field is desiable, cropped sensors will overtake by being able to shoot wide open or at a lower ISO for the same depth of field.

Equivalent Angle of View
------------------------

Angle of view is the horizontal angle a lens sees at, as I mentioned earlier.
MFT has an added caveat: its sensors are 4x3 aspect ratio as opposed to the 3x2 that FF and APS-C have.
This raises the question: what is an equivalent angle of view for MFT compared to FF?

Conventionally, a MFT lens with half the focal length as a FF one will have the same angle of view.
However, this angle of view is contained within a narrower aspect ratio.

I started thinking about this with my new 20mm prime lens for MFT.
Within the FF world, 35mm is a standard lens length — it looks roughly similar to human angle of view with both eyes open.
This corresponds to about 63°.
The MFT equivalent is 17mm, which has an angle of view of 65°.

What happens if we take the aspect ratio into account?
The conversion factor for going MFT to FF is $ \frac{3}{2} \div \frac{4}{3} = \frac{3}{2} \times \frac{3}{4} = \frac{9}{8} $.
Taking this into account, the "equivalent" angle of view of the 17mm MFT lens could be considered to be 73°, which is significantly wider.

Interetingly, the angle of view of my 20mm is 57°, which when multiplied by $ \frac{9}{8} $ is 64° — very close to the FF 35mm.

Is this a better way of thinking about angle of view?
I'm not sure.
But it was a curious thought, and not one I've seen talked about elsewhere.

Conclusion
----------

The word "equivalent" in photography is often used imprecisely.
People should take care to specify what they mean as equivalent — the angle of view, the depth of field, et cetera.

[^coc]: Setting circle of confusion aside, since it is intrinsic to the sensor and not something the photographer can really influence.
[^wpd]: Yes, I know about wave-particle duality.
