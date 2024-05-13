# Csharp-in-android
some csharp api implemention in android。

### Guid

- #### Guid.ToByteArray()

  ```c#
    var guid = new Guid("fc9884a2-06c0-4b6e-9e00-d811f84a83ff");
    byte[] bytes = guid.ToByteArray();
    for (int i = 0; i < bytes.Length; i++)
    {
        Console.WriteLine(bytes[i]);
    }
  ```
    note: bytes in java is signed int while c# is unsigned int.
  ```java
    public static int[] convertToUnsignedArray(byte[] signedArray) {
        int[] unsignedArray = new int[signedArray.length];

        for (int i = 0; i < signedArray.length; i++) {
            unsignedArray[i] = (signedArray[i] & 0xFF);
        }

        return unsignedArray;
    }

    public static int[] toByteArray(UUID uuid) {
        ByteBuffer byteBuffer = ByteBuffer.wrap(new byte[16]);
        byteBuffer.putLong(uuid.getMostSignificantBits());
        byteBuffer.putLong(uuid.getLeastSignificantBits());
        byte[] data = byteBuffer.array();
        byte[] result = new byte[16];
        result[0] = data[3];
        result[1] = data[2];
        result[2] = data[1];
        result[3] = data[0];

        result[4] = data[5];
        result[5] = data[4];
        result[6] = data[7];
        result[7] = data[6];

        result[8] = data[8];
        result[9] = data[9];
        result[10] = data[10];
        result[11] = data[11];
        result[12] = data[12];
        result[13] = data[13];
        result[14] = data[14];
        result[15] = data[15];

        return convertToUnsignedArray(result);
    }

    int bytes = toByteArray(UUID.fromString("fc9884a2-06c0-4b6e-9e00-d811f84a83ff"))；
  ```

### double

- #### double.IsInfinity() and double.IsNaN()

  ```c#
    if(double.IsInfinity(x) || double.IsNaN(x)){
    x = 0;
    }
  ```

  ```java
    if (Double.isInfinite(x) || Double.isNaN(x)) {
            x = 0;
    }
  ```

### string
- #### string format
  ```c#
    var uuid = "2AD1";
    var str = $"0000{ uuid }-0000-1000-8000-00805F9B34FB";
  ```

  ```java
    String uuid = "2AD1";
    String str = String.format("0000%s-0000-1000-8000-00805F9B34FB", uuid);
  ```

### Enum
- #### Flags
  ```c#
  [Flags]
  public enum RowerDataFlag
  {
      MoreData = 1,
      AverageStrokeRate = 2,
      TotalDistance = 4,
      InstantaneousPace = 8,
      AveragePace = 16,
      InstantPower = 32,
      AveragePower = 64,
      ResistanceLevel = 128,
      ExpendedEnergy = 256,
      HeartRate = 512,
      MetabolicEquivalent = 1024,
      ElapsedTime = 2048,
      RemainingTime = 4096,
      SingleEnergy = 8192,
      Pull = 16384,
      ThinkDragFactor = 32768
  }

  RowerDataFlag flags = 465;
  if(flags.HasFlag(RowerDataFlag.MoreData)){
    Console.WriteLine("MoreData");
  }

  if(flags.HasFlag(RowerDataFlag.TotalDistance)){
    Console.WriteLine("TotalDistance");
  }

  if(flags.HasFlag(RowerDataFlag.AveragePower)){
    Console.WriteLine("AveragePower");
  }
  ```
  ```java
    public  class RowerDataFlag {
        public static final int MoreData = 1;
        public static final int AverageStrokeRate = 2;
        public static final int TotalDistance = 4;
        public static final int InstantaneousPace = 8;
        public static final int AveragePace = 16;
        public static final int InstantPower = 32;
        public static final int AveragePower = 64;
        public static final int ResistanceLevel = 128;
        public static final int ExpendedEnergy = 256;
        public static final int HeartRate = 512;
        public static final int MetabolicEquivalent = 1024;
        public static final int ElapsedTime = 2048;
        public static final int RemainingTime = 4096;
        public static final int SingleEnergy = 8192;
        public static final int Pull = 16384;
        public static final int ThinkDragFactor = 32768;

        public static boolean hasFlag(int flags, int flag) {
            return (flags & flag) == flag;
        }
    }

    int flags = 465;
    if(RowerDataFlag.HasFlag(flags,RowerDataFlag.MoreData)){
        System.out.println("MoreData");
    }

    if(RowerDataFlag.HasFlag(flags,RowerDataFlag.TotalDistance)){
        System.out.println("TotalDistance");
    }

    if(RowerDataFlag.HasFlag(flags,RowerDataFlag.AveragePower)){
        System.out.println("AveragePower");
    }
  ```

### DateTime
- #### DateTime format string 
  ```c#
    var str = DateTime.Now.ToString("yyyy-MM-dd HH:mm:ss.fff");
  ```
  ```java
    SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss.SSS");
    sdf.format(new Date());
  ```