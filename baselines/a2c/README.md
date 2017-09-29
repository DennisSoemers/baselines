# A2C

- Original paper: https://arxiv.org/abs/1602.01783
- Baselines blog post: https://blog.openai.com/baselines-acktr-a2c/
- `python -m baselines.a2c.run_atari` runs the algorithm for 40M frames = 10M timesteps on an Atari game. See help (`-h`) for more options.

## A2C

The following text was not in the original OpenAI Baselines repository, but was added in this fork by Dennis Soemers.

#### Summary

- A synchronous variant of A3C. Typically appears to be at least as good or a bit better than A2C, so it seems A3C is no longer fashionable and A2C should be used instead in general?
- Uses multiple different agents acting in copies of the environment at the same time to collect a varied set of experiences. This is an alternative to the experience replay used in DQN with the goal making sure experiences are varied and decorrelated.
- Different agents can use different exploration mechanisms.
- Removing the use of experience replay saves memory, but also enables the use of on-policy and actor-critic RL algorithms, whereas DQN with its experience replay is limited to off-policy RL.
- A3C / A2C are advantage actor-critic methods.
- Maintains a policy `pi(action | state; theta)` and estimate of the value function `V(state; theta_v)`.
- Typically the policy and value function are two separate output layers of otherwise the same neural network (softmax for policy, linear for value).
- Supports discrete and continuous action spaces.

#### Implementation Details

- There is only an example script for atari, not for any continuous-action domains. I suspect that continuous-action domains will require a change in the `utils.sample()` function (called in various places in `policies.py`), which currently has an argmax (which I suppose results in selecting just a single action). Only inspected the code briefly though, didn't actually test this yet.
