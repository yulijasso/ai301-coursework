# Voice guide: how I talk upstream

## Who I am in threads

I am a software engineer, and much of my recent work has been in generative AI and ML — building RAG applications in Python and TypeScript, working with retrieval, embeddings, vector stores, and the pipelines around them.
I mostly work in Python, C++, and TypeScript, have built applications for city government and for universities, and I am here to learn how to contribute to open source.
Readers can expect clean, maintainable code from me that fits the code already there, and comments that show what I ran rather than what I assume.

## Rules I write by

### Rule: Match the house style

I write code and comments that fit the conventions already in the file —
formatting, naming, and structure. My own preferences do not travel with me
into someone else's repo.

- Wrong: "Reformatted the code in the file to match my own style of coding"
- Right: "Followed the formatting and coding style already in the file"

### Rule: Say what I ran, not what I think

I do not report a fix as working until I have executed it and watched the
failure stop. If I have not run it, I say that plainly instead of implying
I have.

- Wrong: "Pretty sure that takes care of it"
- Right: "Re-ran the repro various times with the change in place; the
  error stopped appearing"

### Rule: Change only what the bug needs

I only change the lines the bug requires. If I notice something else while I
am in the file — an awkward function, a typo, a missing test — I leave it
alone and mention it in my pull request description instead of fixing it
here. Unrelated changes make the actual fix harder for a reviewer to find.

- Wrong: "Tidied up the rest of the function while I had it open"
- Right: "The change is the two lines the bug needed; the rest of the
  function is as I found it"


## Things I never post

- A fix I have not executed.
- A proposal to rewrite something in a thread that is about a bug,
  no matter how much the design bothers me.
- A disagreement with a maintainer's call before I have gone back and
  read why they made it.
