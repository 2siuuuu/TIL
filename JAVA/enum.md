
```java
public enum Status {
    DEATH(0),
    LIVE(1),
    // 필요하면 확장: WEAK(2), FLEE(3)
    ;

    private final int code;
    Status(int code) { this.code = code; }
    public int getCode() { return code; }

    public static Status fromString(String s) {
        if (s == null) throw new IllegalArgumentException("status string is null");
        try {
            return Status.valueOf(s.trim().toUpperCase());
        } catch (IllegalArgumentException e) {
            throw new IllegalArgumentException("Invalid status: " + s);
        }
    }

    public static Status fromCode(int code) {
        for (Status st : values()) {
            if (st.code == code) return st;
        }
        throw new IllegalArgumentException("Invalid status code: " + code);
    }
}

```

