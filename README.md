Mouseware uses a cryptographically secure random number generator based on
your mouse movements to generate secure, memorable passwords. Passwords are
generated entirely in the browser, no data is ever sent over the network. The
generated passphrases are similar to those generated by
[Diceware](http://world.std.com/~reinhold/diceware.html) or popularized by
[xkcd](http://xkcd.com/936/), with an emphasis on easy memorization.

We use SHA256 to process the location and timestamp of every mousemove event.
Random words are then selected from noun, adjective and verb word lists to
construct a random sentence. Shannon entropy is reported to estimate password
strength. To avoid a time-consuming mouse moving session on every page load,
we use localStorage to store a seed and initialize our internal entropy buffer
with it on the next load.

To increase entropy when desired, options to replace a randomly chosen letter
with a number or symbol are given. Entropy calculation takes these into
account, and increases the reported entropy by the logarithm of the number of
letters considered for replacement.

Mouseware also provides an alternative markov chain based passphrase generator.
This generator uses a markov chain to generate passphrases that have a similar
structure to normal language, but which doesn't necessarily include actual
English words. These passphrases should be more random for a given length than
the standard mouseware passphrases, but still relatively easy to remember and
to type. This generator also provides an estimated entropy based on the entropy
of the series of nodes visited in the markov chain. Note however, that since
the markov chain generation process makes a series of decisions which is path
dependent, and where the probabilities are not uniform, there is not a simple
mapping from this estimated entropy to the average guesswork required to guess
a passphrase. As a result, the markov chain approach is likely to generate
better passwords for a given length on average. However, if you need very
strong guarantees of the strengths of all passwords, the default algorithm is a
better choice.
