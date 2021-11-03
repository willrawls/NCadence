# NCadence
C# Library to allow a piece of code to be run whenever a timed sequence of keys is pressed

## Example

When I hold down the left control key for around 2 seconds, let go,  then press right shift twice within 1 second, then press right shift again after 5 seconds, run [your code here]

```
public class Example1
{
  public NCadence.Sequencer Sequencer { get; set; }
  public void Setup()
  {
    Sequencer = new NCadence.Sequencer();
    Sequencer.Add(new Cadence()
      .Tolerance(250)                     // Following actions must occur within 250 milliseconds of the listed values
      .PressAndHold(PKey.LControl, 2000)  // User must first hold down the left control key for between 1750-2250 milliseconds
      .KeyPress(PKey.RShift, 2, 1000)     // User must then press and release the right shift key twice between 750-1250 milliseconds
      .Pause(5000).Ish(1000)              // User must press no key of any type for between 4000-6000 milliseconds
      .KeyPress(PKey.RShift)              // User must then press and release the right shift key again within 250-500 milliseconds
      .Call(OnCommand)                    // When all that happens, call OnCommand()
      .MaxRuns(3);                        // But don't allow this to happen more than 3 times`1`1
  }

  public void StartSequencer()
  {
    Sequencer.Enable();
  }

  public void StopSequencer()
  {
    Sequencer.Disable();
  }

  public void OnCommand()
  {
    Console.WriteLine("ding!");
  }
}
