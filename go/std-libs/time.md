✨ 더 깔끔하게 보기 👉🏻 [노션](https://linen-coconut-c8d.notion.site/time-57b8012d169b425999a14cf6c5d78ed1)

# time

> Package time provides functionality for measuring and displaying time.
> 

## `Time`

> an instant in time with nanosecond precision
> 

```go
type Time struct {
	wall uint64       // 1-bit flag, 33-bit sec since 1885, 30-bit nsec
	ext  int64        // extended (elapsed) time information (optional)
	loc  *location    // timezone info
}
```

- wall clock & monotonic clock
    - `wall clock` : time-telling operations
        - time that OS provides
    - `monotonic clock` : time-measuring operations (comparisons, subtractions)
        - offsets from `startNano` (== `runtimeNano() - 1`)
        - all the time using `time.Duration` is implemented based on monotonic clock
        - robust against wall clock resets
- zero value
    
    `January 1, year 1, 00:00:00.000000000 UTC`
    
    `IsZero()`
    
- creation
    - `Now()` : `Local` Time
    - `Date(year, month, day, hour, min, sec, nsec, location)`
    - `Unix(sec, nsec)`
- localization
    
    ### `Location`
    
    > Represents the collection of time offsets in use in a geographical area.
    Maps time instants to the zone in use at that time.
    > 
    - `Local()` `UTC()` `In()` return a `Time` with a specific location
- measuring operations
    - comparison
        - `Before()` `After()`  returns bool
        - `==` : 모든 필드
            - time instant, Location, monotonic clock reading
            - map, db key로 사용할 때 identical location & stripped monotonic reading must be  guaranteed
        - `Equal()` :  time instance value
            
            ```go
            func (t Time) Equal(u Time) bool {
            	if t.wall&u.wall&hasMonotonic != 0 {    // hasMonotonic == 1 << 63
            		return t.ext == u.ext                 
            	}
            	return t.sec() == u.sec() && t.nsec() == u.nsec()
            }
            ```
            
    - calculation
        - `Add()` returns Time
        - `Sub()` returns Duration
            
            ### `Duration`
            
            > the elapsed time between two instants as an int64 nanosecond count
            > 
            
            ```go
            type Duration int64  // elapsed time between two instants nsec count
            ```
            
- formatting
    - `Format(layout string)`
        - returns the formatted textual representation of the time value
        - 다양한 `Layout`을  상수로 제공
            
            ```go
            const (
            	Layout      = "01/02 03:04:05PM '06 -0700" // The reference time, in numerical order.
            	ANSIC       = "Mon Jan _2 15:04:05 2006"
            	UnixDate    = "Mon Jan _2 15:04:05 MST 2006"
            	RubyDate    = "Mon Jan 02 15:04:05 -0700 2006"
            	RFC822      = "02 Jan 06 15:04 MST"
            	RFC822Z     = "02 Jan 06 15:04 -0700" // RFC822 with numeric zone
            	RFC850      = "Monday, 02-Jan-06 15:04:05 MST"
            	RFC1123     = "Mon, 02 Jan 2006 15:04:05 MST"
            	RFC1123Z    = "Mon, 02 Jan 2006 15:04:05 -0700" // RFC1123 with numeric zone
            	RFC3339     = "2006-01-02T15:04:05Z07:00"
            	RFC3339Nano = "2006-01-02T15:04:05.999999999Z07:00"
            	Kitchen     = "3:04PM"
            	// Handy time stamps.
            	Stamp      = "Jan _2 15:04:05"
            	StampMilli = "Jan _2 15:04:05.000"
            	StampMicro = "Jan _2 15:04:05.000000"
            	StampNano  = "Jan _2 15:04:05.000000000"
            )
            ```
            
            [time](https://pkg.go.dev/time#Layout)
            
- parsing
    - `string` → `Time`
        - `Parse(layout, value string)`
            - `layout`에 맞춰 `string` 변환
            - Elements omitted from the layout are assumed to be zero or, when zero is impossible, one
            - zone indicator가 없으면 UTC 기준 Time 반환
            - zone offset이 있으면 UTC + offset Time 반환
            
            → The exact instant used in the representation will differ by the actual zone offset. To avoid such problems, prefer time layouts that use a numeric zone offset, or use ParseInLocation.
            
        - `ParseInLocation(layout, value string, loc *Location)`
            - `ParseInLocation()` : defaultLocation, loc 모두 loc
- 유의점
    - Times should typically store and pass them as values, not pointers
        
        Because... In Go, when some value isn't bigger than one or two words, it's common to simply use it as a value instead of using a pointer. Simply because there's no reason to use a pointer if the object is small and you don't pass it to be changed.
        
        - 예외적으로 pointer를 사용하는 경우 : `json: ",omitempty"` tag
            
            The `omitempty` tag option does not work with `time.Time` as it is a `struct`.
            
            There is a "zero" value for structs, but that is a struct value where all fields have their zero values. This is a "valid" value, so it is not treated as "empty".
            
            ```go
            func isEmptyValue(v reflect.Value) bool {  // encoding/json
            	switch v.Kind() {
            	case reflect.Array, reflect.Map, reflect.Slice, reflect.String:
            		return v.Len() == 0
            	case reflect.Bool:
            		return !v.Bool()
            	case reflect.Int, reflect.Int8, reflect.Int16, reflect.Int32, reflect.Int64:
            		return v.Int() == 0
            	case reflect.Uint, reflect.Uint8, reflect.Uint16, reflect.Uint32, reflect.Uint64, reflect.Uintptr:
            		return v.Uint() == 0
            	case reflect.Float32, reflect.Float64:
            		return v.Float() == 0
            	case reflect.Interface, reflect.Ptr:  // *time.Time
            		return v.IsNil()
            	}
            	return false  // time.Time
            }
            ```
            
    - Time value can be used by multiple goroutines simultaneously except that the methods GobDecode, UnmarshalBinary, UnmarshalJSON and UnmarshalText are not concurrency-safe.

### `Timer`

> Single event : When the timer expires, the current time will be sent on the channel.
> 
- how does it work?
    
    ```go
    // time/sleep.go
    type runtimeTimer struct {
      // same
    }
    
    // runtime/time.go
    type timer struct {
    	pp       uintptr  // heap 구조의 timers에서의 인덱스
    	when     int64
    	period   int64
    	f        func(interface{}, uintptr) // NOTE: must not be closure
    	arg      interface{}
    	seq      uintptr
    	nextwhen int64
    	status   uint32
    }
    ```
    
    ```go
    // time/sleep.go
    func NewTimer(d Duration) *Timer {
        c := make(chan Time, 1)
        t := &Timer{
            C: c,
            r: runtimeTimer{
                when: when(d),
                f:    sendTime,
                arg:  c,
            },
        }
        startTimer(&t.r)
        return t
    }
    ```
    
    Timer wakes up at when, calling f in the timer goroutine.
    

### `Ticker`

> Repeated Multiple events : A Ticker holds a channel that delivers “ticks” of a clock at intervals.
> 
- how does it work?
    
    ```go
    type Ticker struct {
    	C <-chan Time // The channel on which the ticks are delivered.
    	r runtimeTimer
    }
    ```
    
    ```go
    func NewTicker(d Duration) *Ticker {
    	if d <= 0 {
    		panic(errors.New("non-positive interval for NewTicker"))
    	}
    	c := make(chan Time, 1)
    	t := &Ticker{
    		C: c,
    		r: runtimeTimer{
    			when:   when(d),
    			period: int64(d),
    			f:      sendTime,
    			arg:    c,
    		},
    	}
    	startTimer(&t.r)
    	return t
    }
    ```
    
    ```go
    placeT := time.NewTicker(placeDuration)  // duration must be greater than 0
    startT := time.NewTicker(startDuration)  // otherwise, NewTicker() will panic
    sendT := time.NewTicker(sendDuration)
    // ...
    ctx, cancel := context.WithTimeout(context.TODO(), 3*time.Second)
    // ...
    for {
    	select {
    	case <-ctx.Done():  // deadline
    		log.Info().Msg("got shutdown signal")
    		return
    	case <-placeT.C:
    		go sched.Place()
    	case <-startT.C:
    		go sched.Start()
    	case <-sendT.C:
    		go sched.Send()
    	}
    }
    
    ```
