# Interview-Prepration

Given a list of bookings, find the busiest days.

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.ArrayList;
import java.util.Calendar;
import java.util.Collections;
import java.util.Date;
import java.util.HashSet;

public class Solution {
    Solution() {
        long startTime = System.nanoTime();
        SimpleDateFormat ft = new SimpleDateFormat ("yyyy-MM-dd");
        ArrayList<Booking> dates = new ArrayList<Booking>();
        try {
            dates.add(new Booking(ft.parse("2016-10-14"), ft.parse("2016-10-18")));
            dates.add(new Booking(ft.parse("2016-11-11"), ft.parse("2018-12-15")));
            dates.add(new Booking(ft.parse("2016-10-13"), ft.parse("2016-10-14")));
            dates.add(new Booking(ft.parse("2016-10-5"), ft.parse("2016-10-13")));
            dates.add(new Booking(ft.parse("2016-10-12"), ft.parse("2020-10-13")));
            dates.add(new Booking(ft.parse("2016-10-10"), ft.parse("2018-10-13")));
            dates.add(new Booking(ft.parse("2015-10-12"), ft.parse("2016-11-13")));
            dates.add(new Booking(ft.parse("2016-09-12"), ft.parse("2016-12-13")));
            dates.add(new Booking(ft.parse("2016-08-12"), ft.parse("2016-10-18")));
            dates.add(new Booking(ft.parse("2016-10-01"), ft.parse("2016-10-26")));
            dates.add(new Booking(ft.parse("2016-02-03"), ft.parse("2016-10-28")));
            dates.add(new Booking(ft.parse("2016-10-04"), ft.parse("2016-12-28")));
            dates.add(new Booking(ft.parse("2015-10-05"), ft.parse("2056-10-16")));
            dates.add(new Booking(ft.parse("2012-10-12"), ft.parse("2016-10-14")));
            dates.add(new Booking(ft.parse("2011-10-12"), ft.parse("2017-02-18")));
            dates.add(new Booking(ft.parse("2016-10-06"), ft.parse("2018-10-13")));
            dates.add(new Booking(ft.parse("2016-10-12"), ft.parse("2019-10-13")));
        } catch (ParseException e) {
            e.printStackTrace();
        }

        ArrayList<Date> datesMult = new ArrayList<Date>();

        for(Booking b : dates) {
            datesMult.addAll(b.getDates());
        }

        HashSet<Date> datesOnce = new HashSet<Date>(datesMult);

        int highestCount = -1;
        Date mostUsed = new Date();

        for(Date d : datesOnce) {
            int count = Collections.frequency(datesMult, d);
            if(count > highestCount) {
                highestCount = count;
                mostUsed = d;
            }
        }

        System.out.println("The most common used date is " + ft.format(mostUsed) + " and it got used " + highestCount + " times");
        long endTime = System.nanoTime();

        long duration = (endTime - startTime);
        System.out.println("This took " + duration + " nanoseconds");
    }

    private class Booking {
        Date startDate;
        Date endDate;

        Booking(Date d1, Date d2) {
            startDate = d1;
            endDate = d2;
        }

        public ArrayList<Date> getDates() {
            ArrayList<Date> d = new ArrayList<Date>();
            d.add(startDate);
            Calendar c = Calendar.getInstance();
            while(true) {
                c.setTime(startDate);
                c.add(Calendar.DATE, 1);  // number of days to add
                startDate = c.getTime();
                if(startDate.compareTo(endDate) == -1) {
                    d.add(startDate);
                } else if(startDate.compareTo(endDate) == 0) {
                    d.add(endDate);
                    return d;
                }
            }
        }
    }

    public static void main(String[] args) {
        new Solution();
    }
}

