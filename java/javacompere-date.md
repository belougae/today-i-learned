```java
Date now = DateUtil.getDate();


list.removeIf(item -> now.before(item.getStartTime()) || now.after(item.getEndTime()));
替换
list.removeIf(item -> now.compareTo(item.getStartTime()) < 0 || now.compareTo(item.getEndTime()) > 0);
```