---
layout: post
category: Learn
title: Auditing an AI System
description: Supplementing existing software controls for AI system audit.
image: assets/posts/auditing-an-ai-system/splash.jpg
author: tlyleung
---

Machine learning systems are more complex than software systems and as such requires a significant shift in thinking during an audit. In normal software systems, the code is separate from the data. This means that, independent of what data is used as input, the software system doesn't change. Machine learning systems, however, are a function of both code *and* data. Changing the data will result in different model weights and hyperparameters and, consequentially, a different model.
