# DECA Docs

The DECA Project Documentation

## Introduction

A general DECA protocol specification and some example use cases.

##  Requirements

There are some requirements you need to fulfill to be able to work with DECA docs.
 * ```Rust``` >= 1.66
 * ```curl``` >= 7.88.1
 * ```cargo``` >= 1.72.0
 * ```mdBook``` >= v0.4.34
 * ```git``` >= 2.39.2
 
 > NOTE: These are the recommended versions since they were tested in the development environment.


## Installation.

The easiest way to get both Rust and Cargo's latest versions is by using the ```rustup``` script, which also means that you have to use the ```curl``` command.

### 1. Git Installation.

The first step is to install git on you Unix system. To do that,  you only need to run the following command:

```shell
$ sudo apt install git
```

### 2. Curl Installation.

You have to repeat the same proccess to install ```curl```, use the apt command:

```sh
 $ sudo apt install curl
```

   Once you have ```curl``` installed you can go ahead and continue with the Rust and Cargo installations.

###  3. Rust and Cargo Installation.

To install Rust and Cargo on your Unix System you have to download the ```rustup installer script``` using the following command on the terminal:

```shell
$ curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

By using the previous command you will get the latest Rust and Cargo's versions. 

> Suggestion: You can make sure the installation was succesfull by using the following command:
>
> ```sh
> $ rustc --version
> ```
> It tells you the version of Rust that was installed.

> NOTE: Some important considerations when installing Rust:
> 
>  * When you install Rust, it will be installed only for the current user, in other words, the installation is not system-wide.
> 
>  * It is not required to be root or sudo to be able to install Rust.

Once you have completed your Rust and Cargo installations, you can now continue with the ```mdBook``` installation.

### 4. MdBook Installation.

DECA Docs uses ```mdBook``` as a way to create books with Markdown. Since ```mdBook``` is a command line tool, it is ideal for creating tutorials, API documentations, course materials, amongst other useful things.

You can follow the instructions bellow to download ```mdBook```. 

First, you have to use the following command to build and install ```mdBook```:

```shell
$ cargo install mdbook
```

The command will automatically download ```mdBook```, build it and install it in Cargo's global binary directory.

Once installed, the next step is to get the DECA Docs repository. Follow the instructions below to get it.

###  Clone the DECA Documentation repository.

After you have succesfully compleated all installations, you can now access the docummentation repository and contribute to the resources. 
Run the next command on the terminal:

```shell
$ git clone https://git.decentralizedscience.org/DECA/docs.git
```

> * This command lets you copy the DECA Docs repository to your local machine.
> * It also means that you can pull down a full copy of all the repository data that it has at that point in time, including all versions of every file and folder for the project.

Once the repository has been cloned, you can have access to it by entering the following command on your terminal:

```shell
$ cd docs/
```

This command will lead you to the directory where you can find the DECA Docs README.md.

The last step is to run the server using the following command:

```shell
$ mdbook serve 
```

You can view the page on any browser using the following link <http://127.0.0.1:3000>

> NOTE: If you want to access remotely use the `mdbook serve -n 0.0.0.0` which means any IP address can access the DECA Docs project.

## Contribute (Usage)
>ToDo

 

## Contract

* [Telegram](https://t.me/deca_currency/1)
* [Matrix](https://matrix.to/#/#DECA:matrix.org)

***Developers***
- [itzelot01](mailto:itzeltellez59@aragon.unam.mx)

## License

```
Copyright (C) DECENTRALIZED CLIMATE FOUNDATION A.C.
Permission is granted to copy, distribute and/or modify this document
under the terms of the GNU Free Documentation License, Version 1.3
or any later version published by the Free Software Foundation;
with no Invariant Sections, no Front-Cover Texts, and no Back-Cover Texts.
A copy of the license is included in the section entitled "GNU
Free Documentation License". 
```

## References

1. Rust, "Learn Rust", <https://www.rust-lang.org/tools/install>, 2023-08-31.

2. A.Prakash, "How to install Rust and Cargo", <https://itsfoss.com/install-rust-cargo-ubuntu-linux/>, 2023-03-26.

3. The Cargo Book, "Installation", <https://web.mit.edu/rust-lang_v1.25/arch/amd64_ubuntu1404/share/doc/rust/html/cargo/getting-started/installation.html#build-and-install-cargo-from-source>, 2023-08-31.

4. Docs GitHub, "Cloning a repository", <https://docs.github.com/es/repositories/creating-and-managing-repositories/cloning-a-repository>, 2023-08-31.

5. mdBook Docummentation, "Introduction", <https://rust-lang.github.io/mdBook/#:~:text=mdBook%20is%20a%20command%20line,easily%20navigable%20and%20customizable%20presentation.&text=This%20guide%20is%20an%20example%20of%20what%20mdBook%20produces.>, 2023-08-31.
