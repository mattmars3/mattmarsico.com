+++
title = "iced - Introduction"
date = 2026-09-22
+++
Hi, welcome to my tutorial on [iced](https://iced.rs/), a Rust GUI library that has been rising in popularity. I am currently building a music player
application with iced, and had to start from square one with the framework. Given it's a newer library, it was challenging for me to find
a more comprehensive guide to learning the framework so I am hoping this will serve as the resource I wish I had while I was learning. 

Beware, this guide will contain a good bit of code but do not simply gloss over it! It's important to analyze each aspect of the
snippets to understand the importance of each piece. I would also advise you to copy each snippet into your editor and mess around
with the components to test your mental model.

Let's start with the following example. Take a second to familiarize yourself with the view and update functions as they are particularly
important to the architecture of iced.

```rs
use iced::{Background, Element};
use iced::widget::container::background;
use iced::widget::{button, container, text};

#[derive(Debug, Clone)]
pub enum GuiMessage {
    ChangeBackground
}

pub struct GuiState {
    background_color: iced::Color,
}

impl Default for GuiState {
    fn default() -> Self {
        Self {
            background_color: iced::Color::from_rgb(0.0, 1.0, 0.0)
        }
    }
}

fn view(state: &GuiState) -> Element<'_, GuiMessage> {

    let bg_from_state: Background = state.background_color.into();

    container(
        button(text("Change Background")).on_press(GuiMessage::ChangeBackground)
    )
        .padding(20)
        .style(move |_t| background(bg_from_state))
        .into()
}

fn update(state: &mut GuiState, message: GuiMessage) {
    match message {
        GuiMessage::ChangeBackground => {
            state.background_color = iced::Color::from_rgb(1.0, 0.0, 0.0);
        }
    }
}

pub fn main() {
    iced::run(update, view);
}
```

Notice any patterns? If you have used [Elm](https://elm-lang.org/) before you will find this architecture very intuitive; and if you haven't
tried Elm you should go check it out. 

It organizes code into widgets (the design elements / UI itself), interactions (which create messages), and state (which is updated by messages).
I've stolen a diagram from the iced website that describes this particularly well.

<img src="https://book.iced.rs/resources/the-gui-trinity.svg" alt="" class="article-image" />

There is plenty to discuss when it comes to this architecture, if [you're thirsty for more](https://www.youtube.com/watch?v=zymqOEDLYnU),
go check out the [iced Architecture Guide](https://book.iced.rs/architecture.html), as well as the subsequent chapters for more depth.

The rest of this guide is going to provide more practical examples that often follow a question-based flow, hopefully covering everything
from *how can I make a button?* to *how can I write my next app with this?*

*Also please bear with my website since I will be improving the UI and navigation alongside work on this guide.*
