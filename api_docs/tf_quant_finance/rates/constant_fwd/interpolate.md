<!--
This file is generated by a tool. Do not edit directly.
For open-source contributions the docs will be updated automatically.
-->

*Last updated: 2020-04-24.*

<div itemscope itemtype="http://developers.google.com/ReferenceObject">
<meta itemprop="name" content="tf_quant_finance.rates.constant_fwd.interpolate" />
<meta itemprop="path" content="Stable" />
</div>

# tf_quant_finance.rates.constant_fwd.interpolate

<!-- Insert buttons and diff -->

<table class="tfo-notebook-buttons tfo-api" align="left">
</table>

<a target="_blank" href="https://github.com/google/tf-quant-finance/blob/master/tf_quant_finance/rates/constant_fwd/constant_fwd_interpolation.py">View source</a>



Performs the constant forward interpolation for supplied points.

```python
tf_quant_finance.rates.constant_fwd.interpolate(
    interpolation_times, reference_times, reference_yields, dtype=None, name=None
)
```



<!-- Placeholder for "Used in" -->

Given an interest rate yield curve whose maturities and the corresponding
(continuously compounded) yields are in `reference_times` and
`reference_yields`, this function returns interpolated yields at
`interpolation_times` using the constant forward interpolation.

Let `t_i, i=1,...,n` and `y_i, i=1,...,n` denote the reference_times and
reference_yields respectively. If `t` is a maturity for which the
interpolation is desired such that t_{i-1} <= t <= t_i, then constant forward
interpolation produces the corresponding yield, `y_t`, such that the forward
rate in the interval `[t_{i-1},t]` is the same as the forward rate in the
interval `[t_{i-1},t_i]`. Mathematically, this is the same as linearly
interpolating `t*y_t` using the curve `t_i, t_i*y_i`.

`reference_times` must be strictly increasing but `reference_yields` don't
need to be because we don't require the rate curve to be monotonic.

#### Examples

```python
interpolation_times = [1, 3, 6, 7, 8, 15, 18, 25, 30]
# `reference_times` must be increasing, but `reference_yields` don't need to
# be.
reference_times = [0.0, 2.0, 6.0, 8.0, 18.0, 30.0]
reference_yields = [0.01, 0.02, 0.015, 0.014, 0.02, 0.025]
result = interpolate(interpolation_times, reference_times, reference_yields)
```

#### Args:


* <b>`interpolation_times`</b>: The times at which interpolation is desired. A N-D
  `Tensor` of real dtype where the first N-1 dimensions represent the
  batching dimensions.
* <b>`reference_times`</b>: Maturities in the input yield curve. A N-D `Tensor` of
  real dtype where the first N-1 dimensions represent the batching
  dimensions. Should be sorted in increasing order.
* <b>`reference_yields`</b>: Continuously compounded yields corresponding to
  `reference_times`. A N-D `Tensor` of real dtype. Should have the
  compatible shape as `x_data`.
* <b>`dtype`</b>: Optional tf.dtype for `interpolation_times`, reference_times`,
  and `reference_yields`. If not specified, the dtype of the inputs will be
  used.
* <b>`name`</b>: Python str. The name prefixed to the ops created by this function. If
  not supplied, the default name 'constant_fwd_interpolation' is used.


#### Returns:

A N-D `Tensor` of real dtype with the same shape as `interpolations_times`
  containing the interpolated yields.