---
title: "스킵 그램을 텐서플로우로 구현하기 (순한맛)"
classes: wide
math: true
date: 2018-01-03
---

# 스킵 그램을 텐서플로우로 구현하기 (순한맛)

### 스킵 그램이란?

스킵 그램(skip-gram)은 구글에서 제안한 워드 임베딩 모형입니다. 2013년도 발표된 [논문](https://arxiv.org/abs/1301.3781)[^1]에 이론적 근거를 두고 있습니다.

[^1]:해당 논문에서는 CBoW라는 다른 모형도 제시하고 있습니다만, 본 문서에서는 스킵 그램을 다룹니다.

$word2vec$이라는 별칭으로도 알려져 있습니다. 워드 임베딩(word embedding)은 단어(word)를 수백 차원의 벡터 공간에 점(point)으로 표현하는 것 입니다. 즉, 입력 값이 word이고 출력 값이 vector인 문제($word \rightarrow vector$)로 바라볼 수 있기 때문에 $word2vec$이라는 이름이 잘 맞습니다.

스킵 그램은 주변 단어(context)가 유사한 단어들이 벡터 공간상에서 가까워 지게 배치하고자 합니다. 이를 위해 한 단어의 벡터 값으로 주변 단어를 예측하는 모형을 만듭니다. 즉, 한 단어의 벡터는 주변 단어를 추리할 수 있는 값의 집합이 될 것이고, 같은 값을 가지고 있으면 동일한 주변 단어를 예측할 것입니다.[^2]

[^2]:유사한 것은 가깝게, 다른 것은 멀어지도록 학습하기 때문에 어느정도 모형이 학습이 끝나면 어느정도 유사한 단어 벡터는 동일한 주변 단어를 예측하게 될 것입니다.

#### model diagram

