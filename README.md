Hello, I am interested in coding C# and ASP.NET Core MVC 
Find bellow a sample of my code 



public class HomeController : Controller
    {
       ///<summary>
       /// Note for myself , I deleted the oringal index code 
       /// and did something similar to what we did in the  class
       ///</summary>


        /// <summary>
        /// Setting the HTTP GET REQUEST
        /// </summary>
        /// <returns></returns>
        [HttpGet]
        public IActionResult Index()
        {
            ViewBag.MI = 0;
            return View();
        }


        /// <summary>
        /// Setting the HTTP GET POST 
        /// </summary>
        /// <param name="model"></param>
        /// <returns></returns>
        [HttpPost]
        public IActionResult Index(CarLoanCalculatorModel model)
        {
            if (ModelState.IsValid)
            {
                ViewBag.MI = model.CalculateMonthlyInstallmentValue(); // choosing the correct view 
            }
            else
            {
                ViewBag.MI = 0;// Giving value zero to MI 
            }
            return View(model);
        }






 /// <summary>
    /// Setting the properties
    /// </summary>
    public class CarLoanCalculatorModel
    {
        [Required(ErrorMessage = "Please enter car loan amount.")]
        [Range(5000, 30000, ErrorMessage =
               "Car Loan amount must be between 5000 and 30000.")]

        public decimal? CarLoanAmount { get; set; }
      

        [Required(ErrorMessage = "Please enter down payment amount ")]
        public decimal? DownPayment { get; set; }

        [Required(ErrorMessage = "Please enter yearly interest rate.")]
        [Range(0.05, 12.0, ErrorMessage ="Yearly interest rate must be between 0.05 and 12.0")]
        public decimal? YearlyInterestRate { get; set; }

        [Required(ErrorMessage = "Please enter a number of years.")]
        [Range(1, 5, ErrorMessage ="Number of years must be between 1 and 5.")]
        public int? LoanDuration { get; set; }


        /// <summary>
        /// Calculating the formula for montyly installment payment
        /// </summary>
        /// <returns></returns>
        /// 


        /// Note for myself: old method code
        /// decimal? CalculateMonthlyInstallmentValue()
        public decimal? CalculateMonthlyInstallmentValue()
        {
            int? months = LoanDuration * 12;
            decimal? monthlyInterestRate = YearlyInterestRate / 12 / 100;
            decimal? monthlyInstallment = 0;
            decimal? DownPayment = 0;
            for (int i = 0; i < months; i++)
            {
                monthlyInstallment = (monthlyInterestRate)-((CarLoanAmount-DownPayment) + monthlyInterestRate) / (LoanDuration*12);
            }
            return monthlyInstallment;

;

        }
