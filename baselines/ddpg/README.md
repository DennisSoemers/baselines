# DDPG

- Original paper: https://arxiv.org/abs/1509.02971
- Baselines post: https://blog.openai.com/better-exploration-with-parameter-noise/
- `python -m baselines.ddpg.main` runs the algorithm for 1M frames = 10M timesteps on a Mujoco environment. See help (`-h`) for more options.

## DDPG Details

The following text was not in the original OpenAI Baselines repository, but was added in this fork by Dennis Soemers.

#### Summary

- Actor-critic, model-free algorithm based on deterministic policy gradients.
- Supports continuous action spaces (I suppose also discrete? At first glance it seems like it was mainly made to be a ''DQN for continuous action spaces'', but my impression there may be wrong).
- Uses the same insights of DQN to provide stability in learning (replay buffer and target Q network), but now with policy gradients.
