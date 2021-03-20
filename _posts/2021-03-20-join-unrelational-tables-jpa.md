    
    jpa join unrelational table 



        CriteriaBuilder cb = entityManager.getCriteriaBuilder();
        CriteriaQuery<Faiz> query = cb.createQuery(Faiz.class);
        Root<Faiz> faizRoot = query.from(Faiz.class);
        Root<KrediTipKanal> krediTipKanalRoot = query.from(KrediTipKanal.class);
        Root<KrediTipSektor> krediTipSektorRoot = query.from(KrediTipSektor.class);

        query.select(faizRoot)
                .where(
                        cb.equal(faizRoot.get("krediTipId"), krediTipKanalRoot.get("krediTip")),
                        krediTipSektorRoot.get("sektorKod").in("0", "2"),
                        cb.equal(faizRoot.get("krediTipId"), krediTipSektorRoot.get("krediTip")),
                        cb.lessThanOrEqualTo(faizRoot.get("tarih"), LocalDate.now()),
                        cb.greaterThanOrEqualTo(faizRoot.get("bitisTarih"), LocalDate.now()),
                        cb.lessThanOrEqualTo(faizRoot.get("vade"), creditTerm),
                        cb.greaterThanOrEqualTo(faizRoot.get("vadeMax"), creditTerm),
                        cb.lessThanOrEqualTo(faizRoot.get("minCreditAmount"), creditAmount),
                        cb.greaterThanOrEqualTo(faizRoot.get("maxCreditAmount"), creditAmount),
                        cb.equal(krediTipKanalRoot.get("kanal"), onlineChannel)
                );

        final List<Faiz> faizList = entityManager.createQuery(query).getResultList();


    select
        faiz0_.KREDI_TIP as KREDI_TIP1_2_,
        faiz0_.SIRA as SIRA2_2_,
        faiz0_.VADE as VADE3_2_,
        faiz0_.VADE_MAX as VADE_MAX4_2_,
        faiz0_.NORMAL_FAIZ as NORMAL_FAIZ5_2_,
        faiz0_.BITIS_TARIH as BITIS_TARIH6_2_,
        faiz0_.KOMISYON_ORANI as KOMISYON_ORANI7_2_,
        faiz0_.KOMISYON_TUTAR as KOMISYON_TUTAR8_2_,
        faiz0_.KKS_FAIZ_INDIRIMI as KKS_FAIZ_INDIRIMI9_2_,
        faiz0_.UST_LIMIT as UST_LIMIT10_2_,
        faiz0_.MAX_FAIZ as MAX_FAIZ11_2_,
        faiz0_.ALT_LIMIT as ALT_LIMIT12_2_,
        faiz0_.MIN_FAIZ as MIN_FAIZ13_2_,
        faiz0_.REKABETCI_FAIZ as REKABETCI_FAIZ14_2_,
        faiz0_.SATICI_KLUP_FAIZ_INDIRIMI as SATICI_KLUP_FAIZ_15_2_,
        faiz0_.TARIH as TARIH16_2_ 
    from
        FINANS.KO_FAIZ faiz0_ cross 
    join
        FINANS.LK_KREDITIP_KANAL kreditipka1_ cross 
    join
        FINANS.LK_KREDITIP_SEKTOR kreditipse2_ 
    where
        faiz0_.KREDI_TIP=kreditipka1_.KREDI_TIP 
        and (
            kreditipse2_.SEKTOR_KOD in (
                ? , ?
            )
        ) 
        and faiz0_.KREDI_TIP=kreditipse2_.KREDI_TIP 
        and faiz0_.TARIH<=? 
        and faiz0_.BITIS_TARIH>=? 
        and faiz0_.VADE<=24 
        and faiz0_.VADE_MAX>=24 
        and faiz0_.ALT_LIMIT<=25000.00 
        and faiz0_.UST_LIMIT>=25000.00 
        and kreditipka1_.KANAL=?