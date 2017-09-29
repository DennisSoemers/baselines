## If you are curious.

##### Train a Cartpole agent and watch it play once it converges!

Here's a list of commands to run to quickly get a working example:

<img src="../../data/cartpole.gif" width="25%" />


```bash
# Train model and save the results to cartpole_model.pkl
python -m baselines.deepq.experiments.train_cartpole
# Load the model saved in cartpole_model.pkl and visualize the learned policy
python -m baselines.deepq.experiments.enjoy_cartpole
```


Be sure to check out the source code of [both](experiments/train_cartpole.py) [files](experiments/enjoy_cartpole.py)!

## If you wish to apply DQN to solve a problem.

Check out our simple agent trained with one stop shop `deepq.learn` function. 

- [baselines/deepq/experiments/train_cartpole.py](experiments/train_cartpole.py) - train a Cartpole agent.
- [baselines/deepq/experiments/train_pong.py](experiments/train_pong.py) - train a Pong agent using convolutional neural networks.

In particular notice that once `deepq.learn` finishes training it returns `act` function which can be used to select actions in the environment. Once trained you can easily save it and load at later time. For both of the files listed above there are complimentary files `enjoy_cartpole.py` and `enjoy_pong.py` respectively, that load and visualize the learned policy.

## If you wish to experiment with the algorithm

##### Check out the examples


- [baselines/deepq/experiments/custom_cartpole.py](experiments/custom_cartpole.py) - Cartpole training with more fine grained control over the internals of DQN algorithm.
- [baselines/deepq/experiments/atari/train.py](experiments/atari/train.py) - more robust setup for training at scale.


##### Download a pretrained Atari agent

For some research projects it is sometimes useful to have an already trained agent handy. There's a variety of models to choose from. You can list them all by running:

```bash
python -m baselines.deepq.experiments.atari.download_model
```

Once you pick a model, you can download it and visualize the learned policy. Be sure to pass `--dueling` flag to visualization script when using dueling models.

```bash
python -m baselines.deepq.experiments.atari.download_model --blob model-atari-duel-pong-1 --model-dir /tmp/models
python -m baselines.deepq.experiments.atari.enjoy --model-dir /tmp/models/model-atari-duel-pong-1 --env Pong --dueling

```

## DQN Details

The following text was not in the original OpenAI Baselines repository, but was added in this fork by Dennis Soemers.

#### Summary

(source: https://github.com/dennybritz/reinforcement-learning/tree/master/DQN)

- DQN: Q-Learning but with a Deep Neural Network as a function approximator.
- Using a non-linear Deep Neural Network is powerful, but training is unstable if we apply it naively.
- Trick 1 - Experience Replay: Store experience `(S, A, R, S_next)` in a replay buffer and sample minibatches from it to train the network. This decorrelates the data and leads to better data efficiency. In the beginning, the replay buffer is filled with random experience.
- Trick 2 - Target Network: Use a separate network to estimate the TD target. This target network has the same architecture as the function approximator but with frozen parameters. Every T steps (a hyperparameter) the parameters from the Q network are copied to the target network. This leads to more stable training because it keeps the target function fixed (for a while).
- By using a Convolutional Neural Network as the function approximator on raw pixels of Atari games where the score is the reward we can learn to play many of those games at human-like performance.
- Double DQN: Just like regular Q-Learning, DQN tends to overestimate values due to its max operation applied to both selecting and estimating actions. We get around this by using the Q network for selection and the target network for estimation when making updates.

#### Important Limitations

- DQN plays the action corresponding to the output node with the maximum predicted value. This implies that it can only handle environments with discrete actions.

#### Implementation Details

##### Architecture
- Supports regular Multi-Layer Perceptrons using `deepq.models.mlp` and Convolutional Networks (for pixel-input) using `deepq.models.cnn_to_mlp`.
- The CNN also supports a Dueling architecture by setting `dueling=True` in `deepq.models.cnn_to_mlp`. There does not appear to be support for a dueling non-convolutional architecture yet in the implementation. From reading done so far, Dueling seems to be a fairly generally applicable modification that is expected to improve performance in most applications, so it appears that it'll often be useful to set this to `True`.

##### Training
- A model can be trained using `deepq.learn` (which is actually `deepq.simply.learn` due to import from `deepq.__init__.py`).
- Prioritized Replay (instead of uniform sampling from Replay Buffer) is supported using `prioritized_replay=True`

#### Original sources on DQN

- https://storage.googleapis.com/deepmind-media/dqn/DQNNaturePaper.pdf
- https://deepmind.com/research/dqn/
