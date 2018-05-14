In this proposal document, we will outline the desire to re-structure the way
Stingray handles averaging of power spectra and cross spectra.

## The problem:
Light curves of the entire data set are too large to read into memory at once.
This is not only true for new data from NICER, but also for archival RXTE data
used at its intrinsic time resolution. Particularly when the user wants to
average together the power spectrum or cross spectrum of hundreds of segments of
data, it is not possible to store the total light curve in memory.

## One solution: average 'on the fly'
This is the traditional solution, and the one that Abbie is most familiar with.
In this framework, Stingray will read in a segment of data, create a Lightcurve
object, compute `Powerspectrum` and `Crossspectrum`, and keep a running sum
of the power spectrum and cross spectrum as it steps through the segments. At
the end, Stingray will then divide by the number of segments to have the average
power spectrum and cross spectrum.

### Benefits:
* This approach is intuitive for some Stingray users.
* Only need to store one segment of light curve and two segments worth of power
spectra and cross spectra at a time (one for the segment, one for the average).

### Drawbacks:
* Would need to change the input arguments for `AveragePowerspectrum` and
`AverageCrossspectrum`, which would make it not backwards-compatible.

## Another solution: using Dask
Abbie is presently unfamiliar with Dask, though she is aware that it's used to
make storage of and calculations on large arrays more efficient.

### Benefits:
* Fancy

### Drawbacks:
* Requires another dependency.
