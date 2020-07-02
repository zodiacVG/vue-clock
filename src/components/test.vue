if (this.times.hour < 10) { //change to 2 chars fmt
        this.times.hour = "0" + this.times.hour;
    }
    if (this.times.min < 10) {
        this.times.min = "0" + this.times.min;
    }
    if (this.times.sec < 10) {
        this.times.sec = "0" + this.times.sec;
    }
    if (this.times.mon < 10) {
        this.times.mon = "0" + this.times.mon;
    }
    if (this.times.day < 10) {
        this.times.day = "0" + this.times.day;
    }
