- Test and find a better way to return current position, tell to specific point 
  proto: "tell","complete",{position}
         "tell","after","recursion"
- how should last token be handled?
- Replace Browse by a propper wrapping of Typedtree
- Find proper API for incremental parser
  -> goto table should not be manipulated explicitly
  -> exceptions from semantic action should be caught and treated differently
- perf idea: send batches of token rather than entering/exiting the whole
  parser barrier for each token
- backport support for ocaml 4.00 & 4.01
- features to port:
  -> locate
- features to test:
  -> completion
  -> type enclosing / type expr
  -> occurences