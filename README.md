# fastdate
fastdate of Any RFC3339Micro

this date cartes is very fast(<= 50ns) including 
* from_str()
* now()
* utc()
* to_string()/format!()
* eq()
* add()/sub()
* set_offset()

```log
test bench_add            ... bench:          21 ns/iter (+/- 0)
test bench_date_display   ... bench:          44 ns/iter (+/- 0)
test bench_date_now_local ... bench:          40 ns/iter (+/- 1)
test bench_date_parse     ... bench:          10 ns/iter (+/- 0)
test bench_date_utc       ... bench:          39 ns/iter (+/- 0)
test bench_eq             ... bench:           0 ns/iter (+/- 0)
test bench_set_offset     ... bench:          21 ns/iter (+/- 0)
```

* it can from_str for any RFC3339
for example:
```log
1234_12_13_11_12_13.123456
1234-12-13T11:12:13
1234-12-13 11:12:13.123456
1234-12-13T11:12:13.123456
```

* how use?
```rust
use fastdate::DateTime;
fn main(){
    //now with local time zone
    DateTime::now();
    //utc time now
    DateTime::utc();
    // add
    DateTime::now() + Duration::from_secs(1);
    // sub
    DateTime::now() - Duration::from_secs(1);
    //befor,after
    let date1 = DateTime::from_str("2022-12-12 00:00:00").unwrap();
    let date2 = DateTime::from_str("2022-12-12 01:00:00").unwrap();
    assert_eq!(date2.after(&date1), true);
    assert_eq!(date1.before(&date2), true);
    //from str
    let datetime=DateTime::from_str("1234-12-13 11:12:13.123456");
    //from str time zone
    let datetime=DateTime::from_str("1234-12-13 11:12:13.123456+08:00");
    let datetime=DateTime::from_str("1234-12-13 11:12:13.123456Z");
    //parse by format str
    let date = DateTime::parse("hh:mm:ss.000000,YYYY-MM-DD","11:12:14.123456,2022-12-13").unwrap();
    //to_string()
    let s = datetime.to_string();//1234-12-13 11:12:13.123456
    //unix_timestamp
    let timestamp = DateTime::now().unix_timestamp();
    //from unix_timestamp
    let datetime = DateTime::from_timestamp(timestamp);
    //unix_timestamp_millis
    let timestamp = DateTime::now().unix_timestamp_millis();
    //from unix millis
    let datetime = DateTime::from_timestamp_millis(timestamp);
    //unix_timestamp_nano
    let timestamp = DateTime::now().unix_timestamp_nano();
    //from unix_timestamp_nano
    let datetime = DateTime::from_timestamp_nano(timestamp);
}
```
