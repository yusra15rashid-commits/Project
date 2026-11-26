# HFC — Healthy Fry-chicks Ordering Web App

A self-contained, single-file ordering web application built with **HTML**, **CSS**, and **JavaScript** for **HFC (Healthy Fry-chicks)** in Haroonabad. Everything—styles, layout, category data, cart logic, and checkout handling—lives inside `index.html` so it runs directly in any browser or on GitHub Pages without external frameworks or build steps.

## Key Features
- **Interactive Letter Intro (`H`, `F`, `C`):** A black-background splash screen with a yellow wobble transition where tapping `H` or `F` takes visitors to **Hot Deals**, and tapping `C` opens the full **Menu Card**.
- **Categorized Menu & Size Cycling:** Browse categories including Hot Deals, Burgers, Chicken & Wings, Fish & Kababs, Rolls & Shawarma, Special/Crown/Regular Pizzas, Pasta/Rice/Fries, and Water & Ice Cream via the top-right drawer, with corner size toggles (`Small`, `Medium`, `Large`) where available.
- **Slide-Out Cart Drawer:** Add items, adjust quantities (`+` / `−`), clear the cart, and see live totals in PKR (`Rs.`).
- **Checkout & Order Submission:** Dedicated delivery details form with an address reminder pop-up, Formspree submission (`https://formspree.io/f/mgaeegln`), and formatted WhatsApp order links (`+92 343 5871277`).

## Project Structure
```text
├── index.html   # Complete single-file application (HTML, CSS, and JavaScript)
└── README.md    # Project overview and setup notes
