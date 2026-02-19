Latest MRR
Latest MRR = CALCULATE( SUM(monthly_company_kpis[total_mrr]), LASTDATE(monthly_company_kpis[month_start]) )

Previous Month MRR
Previous Month MRR = CALCULATE( SUM(monthly_company_kpis[total_mrr]), DATEADD(monthly_company_kpis[month_start], -1, MONTH) )

MoM MRR Change
MoM MRR Delta = MoM MRR Delta = [Latest MRR] - [Previous Month MRR]

MoM Growth %
MoM Growth % = DIVIDE( [MoM MRR Delta], [Previous Month MRR] )

Rolling 3 Month Churn %
Rolling 3M Churn % = AVERAGEX( DATESINPERIOD( monthly_company_kpis[month_start], MAX(monthly_company_kpis[month_start]), -3, MONTH ), CALCULATE(AVERAGE(monthly_company_kpis[monthly_logo_churn_pct])) )

Net Revenue Retention %
NRR % = VAR CurrentMRR = SUM(monthly_company_kpis[total_mrr]) VAR ChurnMRR = SUM(monthly_company_kpis[churned_mrr]) RETURN DIVIDE(CurrentMRR - ChurnMRR, CurrentMRR) * 100

Churn Risk Status
Churn Risk Status = IF( [Rolling 3M Churn %] > 10, “⚠ Rising Risk”, “Stable” )
