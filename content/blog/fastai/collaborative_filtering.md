---
title: "Collaborative filter from scratch"
date: 2020-07-06T07:08:50+08:00
slug: "Collaborative-filtering-from-scratch"
description: "Building a Collaborative filter from scratch with Pytorch"
keywords: ["Collaborative Filtering", "Pytorch", "AI", "Artificial Intelligence", "FastAI"]
draft: true
tags: ["FastAI", "AI"]
math: false
toc: false
---

Collaborative Filtering is extrapolation of a user's preference to find their preference for other things.

Often, it is used to find out how much one group will like another group and vice versa.

## The Cold Start problem

Often, the times when we want to recommend a product to user is when they are new. (Either the product or the user).

However, that is also the hardest part.

Why?

Because the collaborative filtering model does not have any data in system then.

And without data, it cannot make good decisions.

While there is no one way of solving this problem, one way is to ...

only way Jeremy know of to solve it (in fact, the only way Jeremy thinks that conceptually can solve it) is to have a second model which is not a collaborative filtering model but a metadata-driven model for new users or new movies.

Netflix found like 20 really common movies and asked me if Jeremy liked them, they used his replies to those 20 to show me 20 more that Jeremy might have seen, and by the time he had gone through 60, there was no cold start problem anymore.

for new items, we can change the question and ask if users like the brand // director // artist of that product//movies//song. Then as we get feedback, replace it with the item itself.

## Implementing the Collaborative Filtering Model

```python
def get_embeddings(row_count:int, col_count:int):
    emb = nn.Embedding(row_count, col_count)
    with torch.no_grad():
        # https://arxiv.org/abs/1711.09160
        trunc_normal_(emb.weight, std = 0.01)
    return emb

class EmbeddingDotBias(nn.Module):
    def __init__(self, item_count:int, user_count:int, factor_count:int, y_range:Tuple(float, float) = None):
        super.__init()
        self.y_range = y_range
        (self.user_weight, self.item_weight, self.user_bias, self.item_bias) = [get_embeddings(*size) \
        for size in \
        [(user_count, factor_count), (item_count, factor_count), (user_count, 1), (item_count, 1)]]

    def forward(self, users:LongTensor, items:LongTensor):
        #LongTensor -> signed 64 bit int
        raw_score = self.user_weight(users) * self.item_weight(items)
        final_score = raw_score(1) + self.user_bias(users).squeeze() + self.item_bias(items).squeeze()
        if self.y_range is None:
            return final_score
        else:
            return torch.sigmoid(final_score) * (self.y_range[1] - self.y_range[0]) + self.y_range[0]
```
