# GPU

* GPU = Graphics Processing Unit, so they output graphics (at least for the ones that aren't meant exclusively for cryptomining and calculations: these don't have any display outputs).
* In spite of being relatively less powerful, larger number of GPU cores allow many more relatively basic operations (such as addition, subtraction, multiplication, division) per second.
* Has allowed certain kinds of highly parallelisable math operations to be done on a much larger scale - usefulness depends on specific operations:
  * CNNs (Convolutional Neural Networks) are highly parallelisable by nature, and are the foundation of many image recognition algorithms. Transformers are also considered to be parallelisable: see also [https://ai.stackexchange.com/questions/29903/why-people-always-say-the-transformer-is-parallelizable-while-the-self-attention](https://ai.stackexchange.com/questions/29903/why-people-always-say-the-transformer-is-parallelizable-while-the-self-attention).
  * RNNs (Recurrent Neural Networks), LSTMs and GRUs are less parallelisable by nature: one operation needs to be performed after another. Many algorithms used for Natural Language Processing (NLP) such as text and speech recognition/production depend on operations which are harder to parallelise: see also [https://ai.stackexchange.com/questions/25956/is-the-working-of-rnns-lstm-and-gru-sequential-or-parallel](https://ai.stackexchange.com/questions/25956/is-the-working-of-rnns-lstm-and-gru-sequential-or-parallel).
* Differences in capabilities between different models:
  * TODO!
* Differences between different brands:
  * nVidia:&#x20;
    * Supports CUDA, which AMD and Intel do not: much faster and better supported for machine learning (as of writing)
    * Support for OpenCL lags behind AMD; however the number of libraries supporting OpenCL due to inconsistent implementation and performance across brands means this framework is less useful for ML.&#x20;
    * Linux support is via various drivers:
      * The closed-source one is the highest-performing and most featureful one as of writing. It has stability issues together with some other drivers such as the closed source DisplayLink driver and support varies for some architectures other than x64/x86 and different linux distributions.&#x20;
      * The old open source driver derived from the "nv" driver released by nvidia "nouveau" does not support machine learning and has limitations for 3d acceleration.
  * AMD:&#x20;
    * Supports ROCm and OpenCL. While OpenCL support is much better than nVidia in terms of performance, the two still lag significantly behind nVidia.
    * Linux support is mainly provided by the open source driver, and seems to be stable and performant for games, but less so for machine learning and computations.
  * Intel:
    * TODO!
