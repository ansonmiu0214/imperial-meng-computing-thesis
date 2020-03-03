# Submission Review

## Review 1
* Increase the font size in Figure 1. If Figure 1 was edited carefully by hand, it appears that a readable font size could be used.

> TODO:

* Listing 2: the reader would benefit from an example of client code that uses these types.

> Yes; added forward pointer to Listing 4

* I noted that Listing 4 is related, but Listing 4 inexplicably uses the type Receive_P1, which I think should be the same as S13. Please uses consistent types! (If I'm wrong and Listing 4 is intended to implement something other than S13, consider coordinating your examples more to help the reader).

> Given current implementation, Listing 4 should be S13.

* Also, when describing Listing 2, it would be helpful to say a bit more explicitly that the client is supposed to implement S13, and the code in S13 returns an object of type S15. Then you can point to Listing 4 if they are coordinated.

> OK

* Listing 4 seems to not quite be correct. Shouldn't line 6 return Labels.Update instead of Labels.Draw? 

> Fixed

* Shouldn't lines 4 and 5 return another handleXX function as the third member of the returned tuple?

> No, because they lead to the termination case (sending the move to both players and the session ends)

> TODO: clarify in writing/code?

* A mild criticism of the approach in Listing 4 is that you return "Labels.Draw" but it's not explicit in the code to what component the Draw message is being sent. You can only understand Listing 4 if you also have the protocol to compare against.

> All transitions from an output state must send to the same role, so encoding the role seems to be redundant. However, for the case of the server-side code, I agree that it provides some clarity as part of the code to specify that the message is sent to P2.

> TODO: 

* Section 4, Game server: 2 typos - "as supposed to" (ungrammatical) and "explosions" -> "explosion"

> OK

## Review 2
* The paper overviews such a development's workflow, assuming that the
reader already knows the theory of MPST and (some of) its toolchain.
Even if I think there is no need to further explain the underlying
MPST methodology, the paper should better discuss the specific topics
of the MPST framework that are used in this application. Indeed, the
general explanation is often difficult to follow since it takes for
granted many concepts.

> Ignore?

* The meaning and the usage of EFSM should be explained, as well as what
does it mean to encode EFSM states into TypeScript types.

> Ignore?

* Section 3.1
(and Figure 1) is indeed rather obscure, it is not clear what is
generated on the server-side and what actually is the session runtime.

> TODO: clarify role of session runtime (to execute the EFSM, integrate the user implementation into the sending and receiving of messages)

> Can refer to the concurrent typestates programming paper
for an idea of what the session runtime looks like

* The content of Listing 2 must be definitely explained, showing its
relations to the content of Figure 1 and Listing 1.

> Listing 2 (types) explained with respect to Listing 4 (implementation)

> TODO: link to Figure 1 and Listing 1

* Similarly, in Section 3.2., a simple explanation of the MVU
architecture and the concept of model type are needed.

> TODO: add this (refer to Simon Fowler paper)

## Review 3
* The goal of checking affine channel use requires that the proposed session runtime take complete control of global application control flow. It is not clear to what extent this is compatible with all typical industrial practices.

> ...

* There seems to be a tight coupling in client-side code between user interface events and channel actions. It seems that one would want to allow for some layers of indirection and abstraction between these two. The paper does not seem to address that.

> Separation of concerns (communication logic and program logic)

> ...

* The server-side approach does not seem to allow the server to perform asynchronous operations (e.g. interactions with a database). Since all I/O in Node.js is supposed to happen using asynchronous operations, this effectively means the server cannot do anything but perform protocol actions. This is not discussed by the paper.

> Makes sense; backend tic-tac-toe may want to record plyer move in 
database before proceeding, frontend implementation may make 
external API calls, etc.

> [Backend: ] We can address this by allowing send states to
send values of type T | Promise\<T\>? This way, the session runtime needs to distinguish between the two and handle accordinglyå

> Put "Promise integration" under future work? Unlikely to get something working by next Friday

* Minor question: p.9: could the approach of the present paper be applied in Java as well? Discuss?

> TODO: find citation

> Server-side encoding could be applied to Java. Scribble-Java has some support for the callback-oriented pattern (for branching), except that the session objects are still exposed to the developer.

> TODO: server-side Node.js session runtime possible in Java?
Think so, if we refer to the concurrent TSOP paper, they also 
execute the EFSM internally

- p.1: "Advancements ... has"
> OK
- p.1: "the global ... protocols"
> OK
- p.2: "into mainstream web system"
> OK
- p.3: "does not concern with"
> OK
- p.4: "by preventing the two properties" -> "... conditions"
> OK
- p.5: "the the"
> OK
- p.6: "a event", "a HTML"
> OK
- p.7: "as supposed to" -> "as opposed to"
> OK
- p.8: "as supposed to" -> "as opposed to"; "explosions is" -> "explosion is"
> OK
- p.8-9: "Related/Future Works" -> "... Work"
> OK