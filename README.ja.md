# Torch CRF

PyTorch 0.4 による条件付き確率場 (CRF) の実装

## Requirements

- python 3.6 (python 3.5)
- PyTorch 0.4

## Installation

    pip install git+https://github.com/s14t284/TorchCRF#egg=TorchCRF

## Usage

```python
>>> import torch
>>> from TorchCRF.crf import CRF
>>> batch_size = 2
>>> sequence_size = 3
>>> num_labels = 5
>>> mask = torch.autograd.Variable(torch.FloatTensor([[1, 1, 1], [1, 1, 0]])) # (batch_size. sequence_size)
>>> labels = torch.autograd.Variable(torch.LongTensor([[0, 2, 3], [1, 4, 1]]))  # (batch_size, sequence_size)
>>> hidden = torch.autograd.Variable(torch.randn(batch_size, sequence_size, num_labels), requires_grad=True)
>>> crf = CRF(num_labels)
```

### Computing log-likelihood (順伝搬で使う)

```python
>>> crf.forward(hidden, labels, mask)
tensor([-7.6204, -3.6124], grad_fn=<ThSubBackward>)
```

### Decoding (系列のラベルの予測)

```python
>>> crf.viterbi_decode(hidden, mask)
[[0, 2, 2], [4, 0]]
```

## License

MIT

## References

- [threelittlemonkeys/lstm-crf-pytorch](https://github.com/threelittlemonkeys/lstm-crf-pytorch)
- [kmkurn/pytorch-crf](https://github.com/kmkurn/pytorch-crf)