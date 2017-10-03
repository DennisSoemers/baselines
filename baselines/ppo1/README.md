# PPOSGD

- Original paper: https://arxiv.org/abs/1707.06347
- Baselines blog post: https://blog.openai.com/openai-baselines-ppo/
- `mpirun -np 8 python -m baselines.ppo1.run_atari` runs the algorithm for 40M frames = 10M timesteps on an Atari game. See help (`-h`) for more options.
- `python -m baselines.ppo1.run_mujoco` runs the algorithm for 1M frames on a Mujoco environment.

## PPO Details

The following text was not in the original OpenAI Baselines repository, but was added in this fork by Dennis Soemers.

#### Summary

- Similar to TRPO in spirit (perform updates within a Trust Region), but simpler implementation. This is done using a novel objective function.
- Supports continuous and discrete action spaces.
- Better sample complexity than TRPO (at least empirically)
- The paper looks quite clear at first glance, should take time to read it more thoroughly later.
