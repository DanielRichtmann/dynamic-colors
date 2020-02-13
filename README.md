# dynamic-colors

Utility for changing terminal colors on the fly.

Fork of abandoned [sos4nt/dynamic-colors](https://github.com/sos4nt/dynamic-colors).


## Pre-requisites

Your terminal must support the appropriate OSC escape sequences. xterm and urxvt (rxvt-unicode) work fine, whereas Terminal.app and iTerm won't recognize these sequences.

Make sure `dynamicColors` is enabled in `.Xdefaults`/`.Xresources`

    xterm*dynamicColors: true
    urxvt*dynamicColors: on


### Compatibility Check

Running this command should change your terminal background color to red.

    echo -e "\033]11;#ff0000\007"

Note: this check might not work in tmux. However if it does work outside of tmux, the tool will still work inside of it.


## Setup

1. Clone the repository into `~/.dynamic-colors`:

        git clone https://github.com/sos4nt/dynamic-colors ~/.dynamic-colors

2. Add the tool to your `PATH` by putting following line in your profile (`.bashrc`/`.zshrc`/`.profile`).

        export PATH="$HOME/.dynamic-colors/bin:$PATH"

3. For auto-completion add this to your profile (`.bashrc`/`.zshrc`/`.profile`). Change .zsh to .bash for bash environments.

        source $HOME/.dynamic-colors/completions/dynamic-colors.zsh


## Usage

List available color schemes:

    dynamic-colors list

Switch to a color scheme:

    dynamic-colors switch solarized-dark

Reload last color scheme:

    dynamic-colors init

Add this line to your profile to always set the last color scheme.


### Key binding example for urxvt

Save this to `~/.urxvt/rxt/dynamic-colors`:

    sub on_action {
      my ($self, $cmd) = @_;
      if ($cmd eq "cycle") {
        my $output = `dynamic-colors cycle`;
        $self->cmd_parse($output);
      }
    }

And bind the key in your `~/.Xresources`:

    urxvt*perl-ext-common: dynamic-colors
    urxvt*keysym.F12: dynamic-colors:cycle

Now you can cycle through all color schemes using `F12` without closing running console applications.
