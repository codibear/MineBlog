# android & Server interaction
~~~
package com.example.servicetest.servicetest;

import android.os.Bundle;
import android.support.v7.app.AppCompatActivity;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import org.json.JSONObject;

import okhttp3.MediaType;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.RequestBody;
import okhttp3.Response;

public class MainActivity extends AppCompatActivity {

    private TextView textView ;
    static String responseData;
    private Button button,put,post;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        textView = (TextView)findViewById(R.id.Text);
        button = (Button)findViewById(R.id.button);
        put = (Button)findViewById(R.id.put);
        post = (Button)findViewById(R.id.post);
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                sendRequest();
            }
        });
        put.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                putData();
            }
        });
        post.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                postData();
            }
        });

    }


    private void sendRequest(){
        new Thread(new Runnable() {
        @Override
        public void run() {
            try{
                OkHttpClient client = new OkHttpClient();
                Request request = new Request.Builder()
                        .url("http://lidengming.com:8080/api/v1.0/users/1")
                        .addHeader("1@1.com","123")
                        .build();

                Response response = client.newCall(request).execute();

                String responseData = response.body().string();
                parseJSONWithObject(responseData);
                showResponse(responseData);
                }
            catch (Exception e){e.printStackTrace();}

        }
    }).start();}

    private void postData(){
        new Thread(new Runnable() {
            @Override
            public void run() {
                try{
                    OkHttpClient client = new OkHttpClient();
                    client.authenticator();

                    MediaType mediaType = MediaType.parse("application/json");
                    RequestBody body = RequestBody.create(mediaType, "{\n\t\n}");
                    Request request = new Request.Builder()
                            .url("http://lidengming.com:8080/api/v1.0/studys/")
                            .post(body)
                            .addHeader("content-type", "application/json")
                            .addHeader("authorization", "Basic YmxsbGk6MTIz")
                            .addHeader("cache-control", "no-cache")
                            //.addHeader("postman-token", "5c1ba53d-88b2-1ecd-3cc0-d977b9c715b6")
                            .build();

                    Response response = client.newCall(request).execute();

                    responseData = response.body().string();
                    parseJSONWithPOST(responseData);
                showResponse(responseData);}catch (Exception e){
                    e.printStackTrace();
                }
            }
        }).start();
    }

    private void putData(){
      new Thread(new Runnable() {
          @Override
          public void run() {
              try{
                  OkHttpClient client = new OkHttpClient();
                  MediaType mediaType = MediaType.parse("application/json");
                  RequestBody body = RequestBody.create(mediaType, "{\n\t\n}");
                  Request request = new Request.Builder()
                          .url("http://lidengming.com:8080/api/v1.0/studys/1")
                          .put(body)
                          .addHeader("content-type", "application/json")
                          .addHeader("authorization", "Basic YmxsbGk6MTIz")
                          .addHeader("cache-control", "no-cache")
                          .addHeader("postman-token", "17c29635-eacb-6e88-dc60-c4cdce91423f")
                          .build();

                  Response response = client.newCall(request).execute();
                   responseData = response.body().string();
                  parseJSONWithPUT(responseData);
                  //showResponse(responseData);
              }
              catch (Exception e)
              {
                  e.printStackTrace();
              }
          }
          }).start();
      }

    private void parseJSONWithPOST(String jsonData)
    {
        try{
            JSONObject jsonObject = new JSONObject(jsonData);
            int id = jsonObject.getInt("id");
            String end_time = jsonObject.getString("end_time");
            String start_time = jsonObject.getString("start_time");
            String duration = jsonObject.getString("duration");
           //yishang jie xi zheng que

            StringBuilder stringBuilder = new StringBuilder();
            stringBuilder.append(id);
            stringBuilder.append(end_time);
            stringBuilder.append("start:"+start_time);
            String completedString = stringBuilder.toString();
        }catch (Exception e){e.printStackTrace();}
    }
    private void parseJSONWithObject(String jsonData){
        try{
                JSONObject jsonObject = new JSONObject(jsonData);
                String user = jsonObject.getString("last_seen");
                String study = jsonObject.getString("studys");
                String usersid=jsonObject.getString("username");
                Log.e("Main", "user is :"+user );
                Log.e("Main", "stud"+ study );
                Log.e("Main", "userid "+usersid );

        }catch (Exception e){
            e.printStackTrace();
        }
    }
    private void parseJSONWithPUT(String jsonData){
        try{
            JSONObject jsonObject = new JSONObject(jsonData);
            String message = jsonObject.getString("message");
            showResponse(message);
            Log.e("Main", "msg is :"+message );

        }catch (Exception e){
            e.printStackTrace();
        }
    }

        private void showResponse(final String response)
    {
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                textView.setText(response);
            }
        });
    }
}

~~~

~~~

~~~