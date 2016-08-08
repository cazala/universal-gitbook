# Universal Javascript

The motivation to write this workshop came from the frustration that I found when I had to start working with React + Redux at work. I came from the AngularJS world, and suddenly I had to learn several new concepts and technologies like Webpack, Babel, PostCSS, React, Redux, Enzyme, Server-Side-Rendering, Isomorphic-Javascript, Hot-Module-Replace and a truckload of Other-Fancy-Buzzwords. It took me a while to get my head around this \(I still am\), and a lot of the documentation out there is still very poor... There are many seeds\/starter repos that bring all the stuff together, but after cloning them I would find bigass configuration files which I had no idea how to use, and a lot of glue to hold all the pieces together... So I decided to go ahead and create a short tutorial, starting from scratch, and going thru all the steps from the `npm init` to having a working `universal-server-side-rendered-hot-reloading-isomorphic-react-redux-app`.

I hope if there's someone else going thru the same pain of learning these tecnologies, will finds this useful.

**Prerequisites**

This tutorial assumes you are on a unix machine, with `git` and `nvm` installed. You don't _really_ need them, but they will make your life easier:

* Install [git](https://git-scm.com/book/en/v1/Getting-Started-Installing-Git)

* Install [nvm](http://nvm.sh)


**Fast-forward**

Each chapter of this gitbook has its own **branch** and a **release**, and each section has a **tag** and a **diff**, so you can jump to any part of the tutorial using `git clone` or see the differences between each sections using the diffview on github \(links are provided at the begining of each chapter, and at the end of each section\).
