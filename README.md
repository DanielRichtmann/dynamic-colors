# dynamic-colors

Utility for changing terminal colors on the fly.

Fork of abandoned [sos4nt/dynamic-colors](https://github.com/sos4nt/dynamic-colors).


## Pre-requisites

Your terminal must support the appropriate OSC escape sequences. `xterm` and `urxvt` (rxvt-unicode) work, whereas e.g. `Terminal.app` or `iTerm` won't recognize these sequences.

Make sure `dynamicColors` is enabled in `~/.Xresources`

    xterm*dynamicColors: true
    urxvt*dynamicColors: on


## Setup

1. Add `dynamic-colors` file to your PATH.

2. Put your colorschemes in the configuration directory (commonly `~/.config/dynamic-colors/colorschemes`),
   or set `$DYNAMIC_COLORS_COLORSCHEMES` environment variable to desired path.

3. To enable auto-completion, add this into your shell configuration file:

    source $HOME/.dynamic-colors/completions/dynamic-colors.(zsh|bash)


## Usage

List available color schemes:

    dynamic-colors list

Switch to a color scheme:

    dynamic-colors switch solarized-dark

Reload last color scheme:

    dynamic-colors init


### Key binding example for urxvt

Save this to `~/.urxvt/ext/dynamic-colors`:

    sub on_action {
      my ($self, $cmd) = @_;
      if ($cmd eq "cycle") {
        my $output = `dynamic-colors cycle`;
        $self->cmd_parse($output);
      }
    }

And bind the key in `~/.Xresources`:

    urxvt*perl-ext-common: dynamic-colors
    urxvt*keysym.F12: dynamic-colors:cycle

Now you can cycle through all color schemes using `F12` without closing running console applications.
