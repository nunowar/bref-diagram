<script setup>
import CloudFront from './CloudFront.vue';
import ApiGateway from './ApiGateway.vue';
import S3Bucket from './S3Bucket.vue';
import SQSQueue from './SQSQueue.vue';
import LambdaFunction from './LambdaFunction.vue';
import DatabaseCard from './DatabaseCard.vue';

const lambdaWebInstances = [{ used: 1 }, { used: 1 }, { used: 1 }, { used: 24 }, { used: 24 }, { used: 24 }, { used: 24 }, { used: 20 }, { used: 18 }, { used: 18 }, { used: 18 }, { used: 1 }, { used: 24 }, { used: 24 }, { used: 24 }, { used: 24 }, { used: 20 }, { used: 18 }, { used: 18 }, { used: 18 }, { used: 18 }, { used: 1 }, { used: 24 }, { used: 24 }, { used: 24 }, { used: 24 }];
const lambdaArtisanInstances = [{ used: 24 }, { used: 23 }, { used: 21 }, { used: 19 }, { used: 16 }, { used: 10 }, { used: 6 }, { used: 2 }, { used: 6 }, { used: 2 }];
const lambdaWorkerInstances = [{ used: 20 }, { used: 18 }, { used: 15 }, { used: 12 }, { used: 9 }, { used: 7 }, { used: 4 }, { used: 1 }, { used: 6 }, { used: 2 }, { used: 2 }];
const lambdaWorker2Instances = [{ used: 21 }, { used: 21 }, { used: 19 }, { used: 17 }, { used: 14 }, { used: 11 }, { used: 8 }, { used: 6 }, { used: 3 }];
</script>

<template>
  <div class="relative max-w-7xl rounded-xl bg-gray-50 ring-1 ring-gray-200">
    <div class="flex items-center justify-center p-12" style="background: radial-gradient(circle at center, rgba(0, 0, 0, 0.1) 1px, transparent 1px); background-size: 16px 16px; background-position: center -10px">
      <div class="relative mx-auto grid grid-cols-5 gap-x-6 gap-y-12" style="z-index: 2">
        <!-- level 1 -->
        <div class="col-span-2 flex justify-center">
          <CloudFront :connect-to="['level-2-col-1', 'level-2-col-2']" distribution-id="E1A2B3C4D5E6F7" :nodes="8" flow="output" />
        </div>
        <div class="col-span-3"></div>

        <!-- level 2 -->
        <ApiGateway :connect-to="['level-3-col-1']" flow="both" />
        <S3Bucket name="S3 assets" used-space="56 GB" flow="input" />
        <SQSQueue :grid-col="3" :connect-to="['level-3-col-3', 'level-3-col-4']" name="SQS queue" :messages="1454" :sent-per-second="122" flow="output" />
        <SQSQueue :grid-col="4" :connect-to="['level-3-col-3', 'level-3-col-4']" name="SQS queue-mails" :messages="344" :sent-per-second="222" flow="output" />
        <SQSQueue :grid-col="5" :connect-to="['level-3-col-3', 'level-3-col-4']" name="SQS queue-customer" :messages="454" :sent-per-second="22" flow="output" />

        <!-- level 3 -->
        <LambdaFunction :grid-col="1" :connect-to="['level-4-col-1', 'level-4-col-2', 'level-4-col-3']" name="web" :nodes="8" :instances="lambdaWebInstances" stacked flow="both" />
        <LambdaFunction :grid-col="2" :connect-to="['level-4-col-1', 'level-4-col-2', 'level-4-col-3']" name="artisan" :nodes="8" :instances="lambdaArtisanInstances" stacked flow="output" />
        <LambdaFunction :grid-col="3" :connect-to="['level-4-col-1', 'level-4-col-2', 'level-4-col-3']" name="worker" :nodes="8" :instances="lambdaWorkerInstances" stacked flow="both" />
        <LambdaFunction :grid-col="4" :connect-to="['level-4-col-1', 'level-4-col-2', 'level-4-col-3']" name="worker-2" :nodes="8" :instances="lambdaWorker2Instances" stacked flow="both" />
        <div></div>

        <!-- level 4 -->
        <DatabaseCard type="MySQL 8" storage="1.6 GB" :usage-percent="60" flow="input" />
        <S3Bucket name="S3 storage" used-space="24 GB" flow="input" />
        <S3Bucket name="S3 invoices" used-space="76 GB" flow="input" />
        <div class="col-span-2"></div>
      </div>
    </div>
  </div>
</template>
