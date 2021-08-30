<script>
    const formatter = new Intl.NumberFormat("en-GB", {style: "currency", currency: "GBP"});
    let years = 15;
    let loanAmount = 200000;
    let interestRateInput = 200;
    $: interestRate = interestRateInput / 100;
    $: totalPayments = years * 12;
    $: monthlyInterestRate = (interestRate / 100) / 12;
    $: monthlyPayments = (loanAmount * Math.pow(1 + monthlyInterestRate, totalPayments) * monthlyInterestRate) / (Math.pow(1 + monthlyInterestRate, totalPayments) - 1);
    $: totalPaid = monthlyPayments * totalPayments;
    $: interestPaid = totalPaid - loanAmount;
</script>

<style>

    .container {
        margin: auto;
        padding: 20px;
        border-radius: 8px;
        background-color: rgba(255, 255, 255, 0.8);
        box-shadow: 0 0px 1.2px rgba(0, 0, 0, 0.015),
        0 0px 2.7px rgba(0, 0, 0, 0.022),
        0 0px 4.6px rgba(0, 0, 0, 0.027),
        0 0px 6.9px rgba(0, 0, 0, 0.031),
        0 0px 10px rgba(0, 0, 0, 0.035),
        0 0px 14.2px rgba(0, 0, 0, 0.039),
        0 0px 20.1px rgba(0, 0, 0, 0.043),
        0 0px 29.2px rgba(0, 0, 0, 0.048),
        0 0px 45px rgba(0, 0, 0, 0.055),
        0 0px 80px rgba(0, 0, 0, 0.07);
    }

    .content-wrapper {
        height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .number-input {
        font-size: 20px;
    }


    .outputs {
        font-size: 20px;
        border: solid #98AD90 2px;
        margin-top: 15px;
        text-align: center;
        border-radius: 3px;
    }
</style>

<main class="content-wrapper">
    <div class="container">
        <div class="title row">
            <h1>Mortgage Calculator</h1>
        </div>
        <div class="row">
            <label>Loan Amount</label>
            <input bind:value={loanAmount} min="1" type="number" placeholder="Enter loan amount"
                   class="u-full-width number-input"/>
        </div>
        <div class="row">
            <div class="columns six">
                <label>Years</label>
                <input bind:value={years} type="range" min="1" max="50" class="u-full-width">
            </div>
            <div class="columns six outputs">{years} years</div>
        </div>
        <div class="row">
            <div class="columns six">
                <label>Interest rate</label>
                <input bind:value={interestRateInput} type="range" min="1" max="2000" class="u-full-width">
            </div>
            <div class="columns six outputs">{interestRate.toFixed(2)}%</div>
        </div>

        <div class="row outputs">Monthly Payments {formatter.format(monthlyPayments)}</div>
        <div class="row outputs">Total Paid {formatter.format(totalPaid)}</div>
        <div class="row outputs">Interest Paid {formatter.format(interestPaid)}</div>
    </div>
</main>

