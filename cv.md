# Pankratov Anton Yurievich
#
##### Gmail: _anton.pankratov7526@gmail.com_
##### Telegram: _@an_pa_
##### Discord: _Anton (@Anton-Pankratov)_
#
#
#
### Summary
I like studying and writing beautiful code! I want to be realized in the creativity of programming, create cool products on different platforms and different technologies.
I am currently a practicing programmer with more than 3 years of commercial development experience.

### Skills
Android SDK, Java, Kotlin, MVVM, MVP/Moxy, Single Activity, Retrofit, gRPC, Room, Coroutines, Flow, LiveData, RxJava, Koin, Toothpick, Cicerone, Custom Views, Security and Biometric, some other libraries; Agile, Slack, GitHub, Gitlab, Bitbucket, Jira, Confluence, Greylog.

### Code Example
Based on the state of the response from the server, determine which view and which message to show to the user
```
/** Fetching Status Enum Class */

enum class FetchStatus {
    NONE, FETCHING, SUCCESS_DATA_EXIST, SUCCESS_DATA_EXIST_NOT, FAILURE
}

/** In ViewModel */

private val _status = MutableStateFlow(FetchStatus.NONE)
val status: LiveData<FetchStatus> = _status

fun fetchData() {

    viewModelScope.launch {

    val response = repository.fetchData()
    _status.value = FetchStatus.FETCHING

    when (response) {
        SUCCESS -> {
            val result = response.convertFromJson<List<Data>>()
            if (result.isNullOrEmpty) {
                _status.value = FetchStatus.SUCCESS_DATA_EXIST
                dao.updateData(result)
            } else {
                _status.value = FetchStatus.SUCCESS_DATA_EXIST_NOT
            }
        }
        FAILURE -> {
            _status.value = FetchStatus.FAILURE
        }
    }
}

/** In Fragment */
fun collectFetchStatus() {
    viewLifecycleOwner.lifecycleScope.launch {
        viewModel.status.collect { status ->
            when (status) {
                FetchStatus.FETCHING -> showProgressVIew()
                else -> status.showDialog()
            }
        }
    }
}

fun FetchStatus.showDialog() {
    context.resources.apply {
        when (this) {
            FetchStatus.SUCCESS_DATA_EXIST -> buildDialog(getString(R.string.dialog_data_exist))
            FetchStatus.SUCCESS_DATA_EXIST_NOT -> buildDialog(getString(R.string.dialog_data_not_exist))
            FetchStatus.FAILURE -> buildDialog(getString(R.string.dialog_failure))
        }
    }
}
```

### Work Experience

Middle Android Developer. 3+ years in commercial development.
Developed an internet banking application from scratch (200+ screens) for a large bank in my region.
I am currently working on the development of several fintech applications.

### Education
Self Study + Android Programming Cource in IT-Academy (Bishkek) + Study in work + Videos from World Wide Web.

### English
Reading technical documentation - 3 years. Study in school and university. I want to know it better 😊