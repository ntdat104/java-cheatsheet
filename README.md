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
bsList.stream().sorted(Comparator.comparing(BalanceSheet::getPeriodEndDate))
                .collect(Collectors.toList());
bsList.stream().sorted(Comparator.comparing(BalanceSheet::getPeriodEndDate).reversed())
                .collect(Collectors.toList());
```