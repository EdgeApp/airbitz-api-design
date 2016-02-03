# Airbitz Api Design

# AirbitzException

    class AirbitzException
        boolean isOkay()
        boolean isBadPassword()
        boolean isOtpError()
        ...

# Core 

    class Core
        void initialize(...)
        void uploadLogs()
        string coreVersion()
        void debugLevel(int level, string debugstring)

        void restoreConnectivity()
        void lostConnectivity()

# Account

    class Account
        static List<string> listAccounts()
        static Account signin(username, password)
        static Account createAccount(username, password)
        static boolean deleteAccount(string account)
        static string accountAvailable(string account)
        static double GetPasswordSecondsToCrack(string password)
        List<PasswordRule> GetPasswordRules(string password)

        boolean passwordOK(string password) {
        boolean passwordExists()

        public void callbackAsyncBitcoinInfo(long asyncBitCoinInfo_ptr) {

        boolean isLoggedIn()
        List<string> walletsUuids()
        List<Wallet> wallets()
        void reloadWallets()

        AccountSettings settings()

        boolean bitidLogin(string uri)
        boolean logout()

        string recoveryQuestions()
        void saveRecoveryAnswers(string mQuestions, string mAnswers)
        boolean hasRecoveryQuestionsSet()
        void incRecoveryReminder()
        void clearRecoveryReminder()

        // otp functions
        boolean isTwoFactorOn()
        void otpReset(string username)
        void otpAuthGet()
        void otpKeySet(string username, string secret)
        string getTwoFactorSecret()
        boolean isTwoFactorResetPending(string username)
        void enableTwoFactor(boolean on)
        void cancelTwoFactorRequest()
        string getTwoFactorDate()
        byte[] getTwoFactorQRCode()
        Bitmap getTwoFactorQRCodeBitmap()
        byte[] getQRCode(string uuid, string id)

        string pluginDataGet(string pluginId, string key)
        boolean pluginDataSet(string pluginId, string key, string value)
        boolean pluginDataRemove(string pluginId, string key)
        boolean pluginDataClear(string pluginId)

        void startBackgroundTasks()
        void stopBackgroundTasks()

# AccountSettings

    class AccountSettings:
        boolean saveSettings()

        string GetUserPIN()
        void SetPin(string pin)
        boolean GetDailySpendLimitSetting()
        void SetDailySpendLimitSetting(boolean set)
        long GetDailySpendLimit()
        void SetDailySpendSatoshis(long spendLimit)
        boolean GetPINSpendLimitSetting()
        void SetPINSpendLimitSetting(boolean set)
        long GetPINSpendLimit()
        void SetPINSpendSatoshis(long spendLimit)
        string getDefaultBTCDenomination()
        string getUserBTCSymbol()

# ReceiveRequest

    class ReceiveRequest:
        static ReceiveRequest create(Wallet wallet, string name, string notes, long satoshi)
        boolean finalizeRequest()
        string requestId()
        byte[] qrCode()

        string label
        string notes
        int64_t satoshi
        double currency

# Wallet

    class Wallet
        static Wallet createWallet(Account, walletName, currency)
        boolean removeWallet(string uuid)
        boolean renameWallet(Wallet wallet)

        void incRecoveryReminder()
        void clearRecoveryReminder()
        boolean needsRecoveryReminder(Wallet wallet)

        List<Transaction> transactions()
        Transaction getTransaction(string szTxId)
        List<Transaction> searchTransactionsIn(Wallet wallet, string searchText) {

        long totalSentToday()
        string sweepKey(string wif)
        string getRawTransaction(string txid)
        string getPrivateSeed()
        string getCSVExportData(string uuid, long start, long end)

# Transaction

    class Transaction:
        void save()

        int confirmations()

# SpendTarget

    class SpendTarget:
        boolean newSpend(string text)
        boolean newTransfer(string walletUUID)
        boolean spendNewInternal(string address, string label, string category,
        void setBizId(long bizId)
        void setAmountFiat(double amountFiat)
        string signTx(string walletUUID)
        boolean broadcastTx(string walletUUID, string rawTx)
        string saveTx(string walletUUID, string rawTx)
        string approve(string walletUUID)
        void updateTransaction(string walletUUID, string txId)
        long maxSpendable(string walletUUID)
        long calcSendFees(string walletUUID) throws AirbitzException


# QuestionChoices

    class QuestionChoices:
        static QuestionChoice[] GetQuestionChoices()

# Util

    class Util:
        string formatDefaultCurrency(double in)
        string formatCurrency(double in, int currencyNum, boolean withSymbol)
        string formatCurrency(double in, int currencyNum, boolean withSymbol, int decimalPlaces)
        int userDecimalPlaces()
        string formatSatoshi(long amount)
        string formatSatoshi(long amount, boolean withSymbol)
        string formatSatoshi(long amount, boolean withSymbol, int decimals)

# Left Overs

    public class CoreAPI
        public Wallet getWalletFromUUID(string uuid)
        public Wallet getWalletFromCore(string uuid)
        public string BTCtoFiatConversion(int currencyNum)
        public string FormatDefaultCurrency(long satoshi, boolean btc, boolean withSymbol)
        public string FormatCurrency(long satoshi, int currencyNum, boolean btc, boolean withSymbol)
        public double SatoshiToDefaultCurrency(long satoshi)
        public double SatoshiToCurrency(long satoshi, int currencyNum)
        public long DefaultCurrencyToSatoshi(double currency)
        public long parseFiatToSatoshi(string amount, int currencyNum)
        public long CurrencyToSatoshi(double currency, int currencyNum)
        public boolean TooMuchBitcoin(string bitcoin)
        public boolean TooMuchFiat(string fiat, int currencyNum)

        public boolean hasOTPError()
        public void otpSetError(tABC_CC cc)
        public void otpSetError(AirbitzException error)
        public void otpClearError()

        public string getRequestURI()
        public string getRequestAddress(string uuid, string id)
        public Bitmap getQRCodeBitmap(string uuid, string id)
        public List<string> loadCategories()
        public void addCategory(string strCategory)
        public void removeCategory(string strCategory)
        public boolean isTestNet()
        public static string getSeedData()
        public void prioritizeAddress(string address, string walletUUID)
        public void ChangePassword(string password) throws AirbitzException
        public boolean recoveryAnswers(string strAnswers, string strUserName) throws AirbitzException
        public void ChangePasswordWithRecoveryAnswers(string username, string recoveryAnswers)

        public boolean PinLoginExists(string username)
        public boolean PinLogin(string username, string pin) throws AirbitzException
        public void PinSetup()
        public tABC_CC PinSetupBlocking()
        public void PINLoginDelete(string username)
        public void SetupDefaultCurrency()
        public int defaultCurrencyNum()
        public int getCurrencyNumberFromCode(string currencyCode)
