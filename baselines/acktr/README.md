# ACKTR

- Original paper: https://arxiv.org/abs/1708.05144
- Baselines blog post: https://blog.openai.com/baselines-acktr-a2c/
- `python -m baselines.acktr.run_atari` runs the algorithm for 40M frames = 10M timesteps on an Atari game. See help (`-h`) for more options.

## ACKTR Details

The following text was not in the original OpenAI Baselines repository, but was added in this fork by Dennis Soemers.

#### Summary

Source: mostly the blog post

- Actor-critic (just like, for example, A2C)
- Takes steps in natural gradient direction, making it more sample-efficient than first-order methods such as A2C
- Performs optimization within a trust-region, just like TRPO, leading to increased stability.
- Only a bit more expensive computationally per update than standard gradient updates, much more efficient than TRPO.
- Supports discrete and continuous action spaces.
