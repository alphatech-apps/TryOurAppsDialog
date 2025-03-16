[![](https://jitpack.io/v/alphatech-apps/TryOurAppsDialog.svg)](https://jitpack.io/#alphatech-apps/TryOurAppsDialog)


How to
To get a Git project into your build:

Step 1. Add the JitPack repository to your build file

gradle
gradle.kts
maven
sbt
leiningen
Add it in your root settings.gradle at the end of repositories:

	dependencyResolutionManagement {
		repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
		repositories {
			mavenCentral()
			maven { url 'https://jitpack.io' }
		}
	}
Step 2. Add the dependency

	dependencies {
	        implementation 'com.github.alphatech-apps:TryOurAppsDialog:1.0.1'
	}





public class SplashScreen extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        EdgeToEdge.enable(this);
        setContentView(R.layout.activity_splash_screen);
        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {
            Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);
            return insets;
        });

        AppOpenUtil.countAppOpen(this);

    }




//
// Created by JAKIR HOSSAIN on 3/13/2025.
//
public class DoRemoteJob {
Context context;

    public DoRemoteJob(Context context) {
        this.context = context;

        tryOurOtherAppsLoad();
    }

    public void tryOurOtherAppsLoad() {
        String developerName = context.getString(R.string.developerName);
        new TryOurAppHelper().tryOurOtherAppsLoad(context, developerName, 5); // openCountWant means how much time app open then try to load
    }
}




package com.jakir.tryourappsby5timeappopeneveryday;

public class HomeActivity extends AppCompatActivity {
private final List<TryOurAppsBottomSheet.Appinfo> appList = new ArrayList<>();
private boolean doubleBackPressed = false;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        EdgeToEdge.enable(this);
        setContentView(R.layout.activity_home);
        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {
            Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);
            return insets;
        });

        new DoRemoteJob(this);  // Remote job for load background data

        // Back Pressed Callback
        getOnBackPressedDispatcher().addCallback(this, new OnBackPressedCallback(true) {
            @Override
            public void handleOnBackPressed() {

                // for doubleBackPressed function
                if (doubleBackPressed) {
                    finish(); // Exit the app
                } else {
                    doubleBackPressed = true;
                    Toast.makeText(HomeActivity.this, "Press once again to exit", Toast.LENGTH_SHORT).show();

                    // Check if the rate dialog should be shown
                    if (new TryOurAppHelper().shouldShowTryAppDialog(HomeActivity.this, 6)) {  // openCountWant means how much time app open then try to show
                        new TryOurAppHelper().showTryOurAppsDialog(HomeActivity.this);
                    }
//                  else Toast.makeText(HomeActivity.this, "Exit Dialog Show", Toast.LENGTH_SHORT).show();

                    new Handler(Looper.getMainLooper()).postDelayed(() -> doubleBackPressed = false, 2000);
                }

/*                // for exit dialog function

                // Check if the rate dialog should be shown
                if (new TryOurAppHelper().shouldShowTryAppDialog(HomeActivity.this, 6)) {  // openCountWant means how much time app open then try to show
                    new TryOurAppHelper().showTryOurAppsDialog(HomeActivity.this);
                }else {
                    new Exit_Dialog(this).show();
                }*/
            }
        });
    }
}
