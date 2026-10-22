# A first notebook

```go
import (
	"github.com/go-ndarray/ndarray/random"
	"github.com/go-statistics/stats"
)
```

A thousand draws from seed 42: the
numbers NumPy's `default_rng(42)` gives.

```go
rng := random.DefaultRNG(42)
x, _ := stats.Normal{Loc: 10, Scale: 2}.Rvs(rng, 1000)
```

```go
stats.Percentiles(x, []float64{25, 50, 75}, nil)
```

The same draws in Ruby, through
the go-scikit bindings.

```ruby
fit = Stats::Normal.fit(x)
format("loc %.4f, scale %.4f", fit.loc, fit.scale)
```
