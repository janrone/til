
百分比

```
app:layout_constraintWidth_percent="0.2"
```

动态设置
```
ConstraintLayout.LayoutParams tvYearLayoutParams = (ConstraintLayout.LayoutParams) binding.tvYear.getLayoutParams();
                        tvYearLayoutParams.endToEnd = -1;
                        tvYearLayoutParams.startToStart = -1;

                        if (binding.tvYear.getWidth() < binding.pbYear.getWidth() ) {
                            tvYearLayoutParams.endToEnd = R.id.pb_year;
                        } else {
                            tvYearLayoutParams.startToStart = R.id.pb_year;
                        }
                        binding.tvYear.setLayoutParams(tvYearLayoutParams);
```
