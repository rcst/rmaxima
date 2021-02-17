# rmaxima
Development version of the yet-to-be-released rmaxima CRAN package. rmaxima provides an interface to the powerful and fairly complete maxima computer algebra system

This repository is a fork from the original version created by Ksenila Shumelchyk and Hans W. Borcher [shumelchyk/rmaxima](https://github.com/shumelchyk/rmaxima), which is currently not maintained.

# Installation

## Requirements
- Maxima
- Boost library (>=1.67.0) 

# TODO

- enable loading maxima modules
- Add formatiting functionality: output as tex/mathml-formated string
- Remove unneccassary variable conversions from `std::string` to `boost::filesystem::path` and vice versa
- Portability: fix and test for windows, test for MacOS
- Add documentation

# Changes

## 16.02.2021
- fixed pipe stream synchronisation

## Initial Commit

- MaximaChain.h: changed signature of `MaximaChain::Reply::Reply(std::istream &in)` --> `MaximaChain::Reply::Reply(bp::pistream &in)`
- MaximaChain.cpp changed constructor `MaximaChain::MaximaChain(...)`: `bp::child(maximaPath, args, ctx)`
- MaximaChain.cpp changed all `process->get_stdout()` to is
- Rmaxima.cpp : changed `std::string` `maxpath = bp::find_executable_in_path(maxima");` to `std::string maxpath = bp::search_path("maxima").string();`
- MaximaChain.h: changed class vaiable `size_t pid` to conform with bp::child's: `pid_t pid;`
- MaximaChain.cpp: changed class for setting pid: `pid = process->get_id();` to `pid = process->id()`; --> CAUTION: Still need to fix Windows version!
- MaximaChain.h/cpp: changed `MaximaChain::getId()` signature to return `type bp::pid_t` and `boost::process::pid_t`, respectively
- MaximaChain.h/.cpp: Added a default constructor `Reply::Reply()` cause it is needed and causes "no matching function call `MaximaChain::Reply::Reply()` errror
- MaximaChain.cpp: Substituted all exceptions throws with shortcut Rcpp::stop()-calls
- Rmaxima.cpp: Changed function call `execute`, removed try-catch block
