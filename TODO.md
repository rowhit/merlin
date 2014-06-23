- Replace Browse by a propper wrapping of Typedtree (~60%)
- Find proper API for incremental parser
  -> goto table should not be manipulated explicitly
  -> exceptions from semantic action should be caught and treated differently
  -> relying on special handling of stack bottom is not good either
     Bottom handling code improved, but we should make sure it s stable.
- perf idea: send batches of token rather than entering/exiting the whole
  parser barrier for each token
- backport support for ocaml 4.00 & 4.01
- features to port:
  -> locate
- features to test:
  -> completion
  -> type enclosing / type expr
     An assertion in Type_utils:19 might fail if provided wrong input.
     Some heuristic in type enclosing might generate wrong input and the user
     can deliberately submit something wrong. So this case should receive proper
     treatment.
  -> occurences
- catch "different assumptions" exception
- write syntax error message generating heuristic

DONE
- recovery heuristic is really not sufficient, a few test cases easily trigger
  bad recursion:
  let f =
    let bad
    let x = () in
  fixed in b5cf1991705ea7f2138602875fe774e20b4a0a49

- with this input:
    let xxy =
      let xx = with
    let xxz : int = "hello"

    let _ = xx |;;
  completion at "|" is correct without the preceding "xx", wrong otherwise
  Also, xx generate one expected error and a Not_found exception.
  Both were due to a special case with Pexp_ident in typecore
  fixed in 8f0fd7cf0e5b7c19270c792c4bbda8f067936c5f