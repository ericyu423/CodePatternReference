          class MyApp extends StatelessWidget {
            @override
            Widget build(BuildContext context) {
              return MaterialApp(
                title: 'Week Countdown',
                home: TestPage(),
              );
            }
          }

          class TestPage extends StatelessWidget {
            @override
            Widget build(BuildContext context) {
              return Scaffold(
                appBar: AppBar(title: Text('Week Countdown')),
                body: Center(
                  child: Column(
                    mainAxisSize: MainAxisSize.min,
                    children: <Widget>[
                      Text(
                        '',
                        style: Theme.of(context).textTheme.headline,
                      ),
                      WeekCountdown()
                    ],
                  ),
                ),
              );
            }
          }

          class WeekCountdown extends StatefulWidget {
            @override
            State<StatefulWidget> createState() => _WeekCountdownState();
          }

          class _WeekCountdownState extends State<WeekCountdown> {
            Timer _timer;
            DateTime _currentTime;

            @override
            void initState() {
              super.initState();
              _currentTime = DateTime.now();
              _timer = Timer.periodic(Duration(seconds: 1), _onTimeChange);
            }

            @override
            void dispose() {
              _timer.cancel();
              super.dispose();
            }

            void _onTimeChange(Timer timer) {
              setState(() {
                _currentTime = DateTime.now();
              });
            }

            @override
            Widget build(BuildContext context) {
              final startOfNextWeek = calculateStartOfNextWeek(_currentTime);
              final remaining = startOfNextWeek.difference(_currentTime);

              final days = remaining.inDays;
              final hours = remaining.inHours - remaining.inDays * 24;
              final minutes = remaining.inMinutes - remaining.inHours * 60;
              final seconds = remaining.inSeconds - remaining.inMinutes * 60;

              final formattedRemaining = '$days Days : $hours Hours : $minutes Mins : $seconds';

              return Text(formattedRemaining, style: new TextStyle(
                        fontFamily: "Roboto",
                        fontSize: 20.0,
                      ), );
            }
          }

          DateTime calculateStartOfNextWeek(DateTime time) {
            final daysUntilNextWeek = 8 - time.weekday;
            return DateTime(time.year, time.month, time.day + daysUntilNextWeek);
          }
