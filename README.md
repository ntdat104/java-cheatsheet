# java cheat sheet

---

## 1. groupingBy
```java
Map<String, List<PriceHistoryDto>> mapPriceData = new TreeMap<>(priceAndMarketList.stream().collect(Collectors.groupingBy(PriceHistoryDto::getDate)));

Map<String, List<PriceHistoryDto>> mapPriceData = new TreeMap<>(priceAndMarketList.stream().collect(Collectors.groupingBy((o) -> DateUtil.parseDateYYMMString(o.getDate()))));
```

## 2. mapToDouble
```java
double[] values = result.stream().mapToDouble(TimeSeriesNumberView::getValue).toArray();
```

## 3. max
```java
BodMemberItemDto selectedDto = dtos.stream().max(Comparator.comparingDouble(BodMemberItemDto::getTenure)).orElse(dtos.get(0));
```

## 4. toMap
```java
Map<Long, AggregateAnalysis> companyMap = companies.stream().collect(Collectors.toMap(p -> p.getCompany().getId(), item -> item));
```

## 5. limit
```java
List<AggregateAnalysis> agg = aggregateAnalysisRepository.findByTickerIn(mapTickers.keySet().stream().limit(4).collect(Collectors.toList()));
```

## 6. noneMatch
```java
List<AggregateAnalysis> top2RelatedCompanyMarketCap = topRelatedCompanyMarketCap.stream().filter(p -> (p.getIsDelisted() == null || p.getIsDelisted() != 1) &&  !p.getTicker().equals(currentTicker.getTicker())
        && companyRelatedDtos.stream().noneMatch(o -> o.getTicker().equals(p.getTicker()))).limit(12-companyRelatedDtos.size()).collect(Collectors.toList());
```

## 7. anyMatch
```java
opPredicteds.stream().anyMatch(p -> p.getDpsFuture() != null)
```

## 8. allMatch
```java
boolean isCashDividendAnnualized3Y  = !CollectionUtils.isEmpty(lastTop3) && lastTop3.size() >=3 && lastTop3.stream().allMatch( p -> p.getCashDividendAnnualized() > 0);
```

## 9. min + naturalOrder
```java
Date minDate = separateShare.stream().map(SeparateShare::getDate).min(Comparator.naturalOrder()).orElse(null);
```

## 10. sorted
```java
1. Sorting an Array
Integer[] numbers = {5, 1, 4, 2, 3};
Arrays.sort(numbers);
Arrays.sort(numbers, Collections.reverseOrder());

Integer[] numbers = {5, 1, 4, 2, null, 3};
Arrays.sort(numbers, (a, b) -> {
        if (a == null) return 1;
        if (b == null) return -1;
        return b.compareTo(a);
});

2. Sorting a List
List<Integer> numbers = Arrays.asList(5, 1, 4, 2, 3);
Collections.sort(numbers);
Collections.sort(numbers, Collections.reverseOrder());

List<Integer> numbers = Arrays.asList(5, 1, 4, 2, null, 3);
Collections.sort(numbers, (a, b) -> {
        if (a == null) return 1;
        if (b == null) return -1; 
        return b.compareTo(a);
});

3. Sorting with Custom Comparator
List<Person> people = Arrays.asList(
            new Person("Alice", 30),
            new Person("Bob", 25),
            new Person("Charlie", 35)
        );
Collections.sort(people, new Comparator<Person>() {
        @Override
        public int compare(Person p1, Person p2) {
        return Integer.compare(p1.age, p2.age);
        }
});

4. Using Java 8+ Lambda Expressions
List<Person> people = Arrays.asList(
        new Person("Alice", 30),
        new Person("Bob", 25),
        new Person("Charlie", 35)
);
people.sort((p1, p2) -> p1.name.compareTo(p2.name));
people.sort((p1, p2) -> p1.age - p2.age);

5. Advanced Sorting by Multiple Fields
List<Person> people = Arrays.asList(
        new Person("Alice", 30),
        new Person("Bob", 25),
        new Person("Charlie", 30),
        new Person("David", 25)
);
people.sort(Comparator.comparingInt((Person p) -> p.age)
                        .thenComparing(p -> p.name));
// Reverse the sorted list
Collections.reverse(people);
people.sort(Comparator.comparingInt((Person p) -> p.age)
                        .thenComparing(p -> p.name)
                        .reversed());
people.sort(Comparator.comparingInt((Person p) -> p.age).reversed()
                              .thenComparing(p -> p.name));

List<Person> people = Arrays.asList(
        new Person("Charlie", 30),
                null,
        new Person("David", 25),
                null,
        new Person("Alice", 30),
        new Person("Bob", 25)
);
people.sort(Comparator.nullsLast(Comparator.comparingInt((Person p) -> p.age)
                                .thenComparing(p -> p.name).reversed()));

5. Sort with stream to create new ArrayList
bsList.stream().sorted(Comparator.comparing(BalanceSheet::getPeriodEndDate))
                .collect(Collectors.toList());
bsList.stream().sorted(Comparator.comparing(BalanceSheet::getPeriodEndDate).reversed())
                .collect(Collectors.toList());
```