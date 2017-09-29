# trpo_mpi

- Original paper: https://arxiv.org/abs/1502.05477
- Baselines blog post: https://blog.openai.com/openai-baselines-ppo/
- `mpirun -np 16 python -m baselines.trpo_mpi.run_atari` runs the algorithm for 40M frames = 10M timesteps on an Atari game. See help (`-h`) for more options.
- `python -m baselines.trpo_mpi.run_mujoco` runs the algorithm for 1M timesteps on a Mujoco environment.

## TRPO Details

The following text was not in the original OpenAI Baselines repository, but was added in this fork by Dennis Soemers.

#### Summary

- The TRPO paper first describes an approach (kind of like a policy gradient approach) that is proven to lead to step-wise policy improvements.
- The final algorithm uses various approximations for terms in this theoretically justified algorithm to create a practical algorithm.
- Intuitively, it only makes steps within a certain region (the ''Trust Region') around the current policy, such that the algorithm is fairly sure about its approximations still being accurate.
- According to [http://www.cs.toronto.edu/~tingwuwang/trpo.pdf](http://www.cs.toronto.edu/~tingwuwang/trpo.pdf), a successful baseline for locomotion tasks
- Requires little tuning of hyperparameters according to original paper
- Supports continuous and discrete action spaces

#### Important Limitations

According to [http://www.cs.toronto.edu/~tingwuwang/trpo.pdf](http://www.cs.toronto.edu/~tingwuwang/trpo.pdf):

- Sample-inefficient (typically requires lots of samples) (according to above link)
- Unable to scale to large networks (according to link above)
