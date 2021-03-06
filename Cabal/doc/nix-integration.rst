Nix Integration
===============

`Nix <http://nixos.org/nix/>`_ is a package manager popular with some Haskell developers due to its focus on reliability and reproducibility. ``cabal`` now has the ability to integrate with Nix for dependency management during local package development.

Enabling Nix Integration
------------------------

To enable Nix integration, simply pass the ``--enable-nix`` global option when you call ``cabal``. To use this option everywhere, edit your ``$HOME/.cabal/config`` file to include:

.. code-block:: cabal

    nix: True

If the package (which must be locally unpacked) provides a ``shell.nix`` file, this flag will cause ``cabal`` to run most commands through ``nix-shell``. The following commands are affected:

- ``cabal configure``
- ``cabal build``
- ``cabal repl``
- ``cabal install`` (only if installing into a sandbox)
- ``cabal haddock``
- ``cabal freeze``
- ``cabal gen-bounds``
- ``cabal run``

If the package does not provide a ``shell.nix``, ``cabal`` runs normally.

Creating Nix Expressions
------------------------

The Nix package manager is based on a lazy, pure, functional programming language; packages are defined by expressions in this language. The fastest way to create a Nix expression for a Cabal package is with the `cabal2nix <https://github.com/NixOS/cabal2nix>`_ tool. To create a ``shell.nix`` expression for the package in the current directory, run this command:

.. code-block:: console

    $ cabal2nix --shell ./. >shell.nix

Further Reading
----------------

The `Nix manual <http://nixos.org/nix/manual/#chap-writing-nix-expressions>`_ provides further instructions for writing Nix expressions. The `Nixpkgs manual <http://nixos.org/nixpkgs/manual/#users-guide-to-the-haskell-infrastructure>`_ describes the infrastructure provided for Haskell packages.
