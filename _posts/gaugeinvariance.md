Title: The beauty of Local Gauge Invariance
Date: 2019-12-12
Category: Theoretical Physics
Summary: One of the most interesting things you'll see in physics is that symmetry and beauty give rise to the fundamental forces of nature.
tags: theoretical physics, gauge theories, electromagnetism, quantum electrodynamics

Our current understanding of the fundamental nature of reality is deeply tied with the concept of symmetry.
One of my favourite mathematicians is Emmy Noether. Her theorem, which states that
every symmetry that exists in any laws of physics is associated to a conserved quantity, is one of the most
beautiful and fundamental statements in all of physics. In fact, there is an entire field in mathematics
that studies the sets of transformations (or groups) that act on a certain space X while still leaving it
invariant, it's called *Group Theory* and it is essential to **Standard Model of Particle physics**
which is based on what is called *Gauge theories*.

> In physics, a gauge theory is a type of field theory in which the Lagrangian does not change (is invariant)
under local transformations from certain Lie groups
>
> -- <cite>Wikipedia</cite>

Given a certain Lagrangian density (for a free fermion field $\psi$ for example), one could attempt to
find the sets of different transformations in which it is invariant. In this post we will do just that
and see that it leads to surprising results!

## Global Symmetry

Let's start simple. The Lagrangian density of a Dirac Bi-spinor field is:
$$\cal{L}_{\textit{Dirac}} = \hbar c \overline{\psi} \gamma^\mu \partial_\mu \psi + mc^2\overline{\psi}\psi$$
Applying the Euler-Lagrange equations would give us the famous *Dirac Equation*, but we're not interested
in that right now. We want to see if there are any transformations which leave this Lagrangian invariant.
To start off, we'll try one of the simplest possible transformations, a global phase-shift. This
basically amounts to changing the phase of the field by the same amount everywhere and is equivalent
to rotating around the unit circle in complex space: $$\psi \rightarrow \psi' = e^{iq\phi}\psi$$
A minor detail that we will need is that the Dirac adjoint is defined as $\overline{\psi} = i \psi^\dagger
\gamma^0$ and it transforms like so:

$$\overline{\psi} \rightarrow \overline{\psi}' = \overline{\psi} e^{-iq\phi}$$

Plugging this new transformed field in to the Lagrangian:
$$\cal{L}' = \hbar c \overline{\psi}' \gamma^\mu \partial_\mu \psi' + mc^2\overline{\psi}'\psi'$$
$$\cal{L}' = \hbar c \overline{\psi} e^{-iq\phi} \gamma^\mu \partial_\mu e^{iq\phi}\psi + mc^2 \overline{\psi} e^{-iq\phi} e^{iq\phi} \psi$$

Now $e^{iq\phi}$ and $e^{-iq\phi}$ are just complex phases and have no spacetime dependance so we can
just move them next to eachother, they cancel out and our Lagrangian is invariant:
$$\cal{L}' = \hbar c \overline{\psi} \gamma^\mu \partial_\mu \psi + mc^2\overline{\psi}\psi = \cal{L}$$

## Local Symmetry

It turns out our Lagrangian is already symmetric under this global transformation, but it doesn't take
us very far. *Gauge theories* for some reason arise when we try to enforce symmetry under **Local
Transformations**. Let's what that looks like:
$$\psi \rightarrow \psi' = e^{iq\phi(x^\mu)}\psi \qquad \overline{\psi} \rightarrow \overline{\psi}' = \overline{\psi} e^{-iq\phi(x^\mu)}$$

In a way this is a "stronger" constraint because we could just get back the global transformation by
using a constant $\phi(x^\mu)$. But now our transformation can be local because it depends on where we
are in spacetime. Depending on the function $\phi(x^\mu)$, we could really mess up the $\psi$ field.
I can already hear you mumbling *"that's all well and good but what the blazes is that gonna achieve?"*,
but let's try it anyway:

$$\mathcal{L}' = \hbar c \overline{\psi} e^{-iq\phi(x^\mu)} \gamma^\mu \partial_\mu e^{iq\phi(x^\mu)}\psi + mc^2 \overline{\psi} e^{-iq\phi(x^\mu)} e^{iq\phi(x^\mu)} \psi$$
$$\mathcal{L}' = \hbar c \overline{\psi} e^{-iq\phi(x^\mu)} \gamma^\mu \partial_\mu(e^{iq\phi(x^\mu)}\psi) + mc^2 \overline{\psi} \psi$$
$$\mathcal{L}' = \hbar c \overline{\psi} e^{-iq\phi(x^\mu)} \gamma^\mu e^{iq\phi(x^\mu)} \partial_\mu\psi + iq\hbar c \overline{\psi} e^{-iq\phi(x^\mu)} \gamma^\mu e^{iq\phi(x^\mu)} \partial_\mu\phi(x^\mu) \psi + mc^2 \overline{\psi} \psi$$
Not so good but let's go further..
$$\mathcal{L}' = \hbar c \overline{\psi} \gamma^\mu \partial_\mu\psi + iq\hbar c \overline{\psi} \gamma^\mu \partial_\mu\phi(x^\mu) \psi + mc^2 \overline{\psi} \psi$$

So the mass term is invariant just like before, but now since the phase-shift depends on position, we cannot
simply move it past the derivative $\partial_\mu$ like last time, we get that pesky middle term with
$\partial_\mu\phi(x^\mu)$. Seems like a bust, unless..
---
Let's do something crazy, we clearly have an issue with $\partial_\mu$ so let's mess it up in just the right
way. Introducing $D_\mu = \partial_\mu + iqA_\mu$ where $A_\mu \rightarrow A_\mu '$. The Lagrangian becomes:
$$\mathcal{L} =\hbar c \overline{\psi} \gamma^\mu \partial_\mu\psi + iq\hbar c \overline{\psi} \gamma^\mu A_\mu \psi + mc^2 \overline{\psi} \psi$$
We can clearly make this invariant if: $A_\mu \rightarrow A_\mu ' = A_\mu - \partial_\mu \phi(x^\mu)$
Using the same process as before:

$$\mathcal{L'} = \hbar c \overline{\psi} \gamma^\mu \partial_\mu\psi + iq\hbar c \overline{\psi} \gamma^\mu A_\mu \psi + iq\hbar c \overline{\psi} \gamma^\mu \partial_\mu \phi(x^\mu) \psi - iq\hbar c \overline{\psi} \gamma^\mu \partial_\mu \phi(x^\mu) \psi + mc^2 \overline{\psi} \psi$$
$$\mathcal{L'} =\hbar c \overline{\psi} \gamma^\mu \partial_\mu\psi + iq\hbar c \overline{\psi} \gamma^\mu A_\mu \psi + mc^2 \overline{\psi} \psi = \mathcal{L}$$

So we managed to make the Lagrangian invariant but look! The new field is interacting with our
Dirac field in the term $iq\hbar c \overline{\psi} \gamma^\mu A_\mu \psi$, and there's a weird coupling
constant $q$ dictating the strength of the interaction. What does this mean?

We do know of a field that behaves in this specific way.

Behold! The **Electromagnetic Field**!
In fact, $A_\mu$ is the *E&M* four-potential $A^\mu = (\phi, \vec{A})$. The weird constant $q$ is nothing
but **electric charge**! It seems obvious now that it should be the coupling strength of the *E&M* field
with the Dirac field. We insisted on a symmetry we had no right to, and rediscovered electromagnetism
in its quantum nature. Isn't that mindblowing?

## Tying up some loose ends

Since $A_\mu$ is now a field itself, it needs to play by the rules of Special Relativity, a.k.a obey
the Klein-Gordon equation which arises from the Proca Lagrangian:
$$\mathcal{L}_\textit{Proca} = \frac{1}{16\pi} F_{\mu\nu} F^{\mu\nu} + \frac{1}{8\pi} (\frac{mc^2}{\hbar}) A^\mu A_\mu$$
The first term is already invariant, but we need to eliminate the second term to make the whole Lagrangian
invariant by setting $m = 0$. This is to be expected because excitations in the E&M field (a.k.a photons)
are massless. Hence, our new full-blown Lagrangian of **Quantum Electrodynamics** is:
$$\mathcal{L}_\text{QED} = \hbar c \overline{\psi} \gamma^\mu \partial_\mu\psi + iq\hbar c \overline{\psi} \gamma^\mu A_\mu \psi + mc^2 \overline{\psi} \psi + \frac{1}{16\pi} F_{\mu\nu} F^{\mu\nu}$$
We can construct the well known antisymmetric *Electromagnetic Field Tensor* as follows:
$$F_{\mu\nu} = \partial_\mu A_\nu - \partial_\nu A_\mu$$
When we imposed $A_\mu \rightarrow A_\mu ' = A_\mu - \partial_\mu(\phi)$, that is nothing but the Lorenz
Gauge condition from classical electrodynamics.

Just for the sake of closure, and because you can never go wrong with them, Maxwell's equations
can be pulled from the QED Lagrangian by applying the Euler-Lagrange equations for $A_\mu$
where the four-current is defined as $J^\mu = (c\rho, \vec{j})$:
$$\partial_\mu F^{\alpha \beta} = \mu_0 J^{\beta}$$

## Epilogue
Let's recap, we started with a simple free Lagrangian density which was already symmetric under global
phase shifts. We tried to impose local gauge symmetry which, a priori, we have no right to expect should
work. It turns out, this local gauge symmetry imposes the conservation of a certain quantity, and that is
electric charge.

We tried one trick and we got the Electromagnetic field, Electric charge, Quantum Electrodynamics and the kitchen sink!
