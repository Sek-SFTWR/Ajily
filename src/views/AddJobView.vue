<script setup>
import router from "@/router";
import { reactive } from "vue";
import { useToast } from "vue-toastification";
import axios from "axios";

const form = reactive({
  type: "Бүтэн цагийн",
  title: "",
  description: "",
  salary: "",
  location: "",
  company: {
    name: "",
    description: "",
    contactEmail: "",
    contactPhone: "",
  },
});

const toast = useToast();

const handleSubmit = async () => {
  const newJob = {
    title: form.title,
    type: form.type,
    location: form.location,
    description: form.description,
    salary: form.salary,
    company: {
      name: form.company.name,
      description: form.company.description,
      contactEmail: form.company.contactEmail,
      contactPhone: form.company.contactPhone,
    },
  };

  try {
    await new Promise((resolve) => setTimeout(resolve, 1000));
    const response = await axios.post("http://localhost:5000/jobs", newJob);
    toast.success("Ажлын байр амжилттай нэмэгдлээ");
    router.push(`/jobs/${response.data.id}`);
  } catch (error) {
    console.error("Ажлын байр нэмэхэд алдаа гарлаа", error);
    toast.error("Ажлын байр нэмэгдсэнгүй");
  }
};
</script>

<template>
  <section class="bg-green-50">
    <div class="container m-auto max-w-2xl py-24">
      <div
        class="bg-white px-6 py-8 mb-4 shadow-md rounded-md border m-4 md:m-0"
      >
        <form @submit.prevent="handleSubmit">
          <h2 class="text-3xl text-center font-semibold mb-6">
            Ажлын байр нэмэх
          </h2>

          <div class="mb-4">
            <label for="type" class="block text-gray-700 font-bold mb-2"
              >Ажлын төрөл</label
            >
            <select
              v-model="form.type"
              id="type"
              name="type"
              class="border rounded w-full py-2 px-3"
              required
            >
              <option value="Бүтэн цагийн">Бүтэн цагийн</option>
              <option value="Хагас цагийн">Хагас цагийн</option>
              <option value="Алсаас">Алсаас</option>
              <option value="Дадлага">Дадлага</option>
            </select>
          </div>

          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2"
              >Ажлын байрны нэр</label
            >
            <input
              type="text"
              v-model="form.title"
              id="name"
              name="name"
              class="border rounded w-full py-2 px-3 mb-2"
              placeholder="Жишээ нь: Майамид байршилтай гоё орон сууц"
              required
            />
          </div>
          <div class="mb-4">
            <label for="description" class="block text-gray-700 font-bold mb-2"
              >Тайлбар</label
            >
            <textarea
              id="description"
              v-model="form.description"
              name="description"
              class="border rounded w-full py-2 px-3"
              rows="4"
              placeholder="Ажлын үүрэг, шаардлага, бусад зүйлийг нэмээрэй"
            ></textarea>
          </div>

          <div class="mb-4">
            <label for="type" class="block text-gray-700 font-bold mb-2"
              >Цалин</label
            >
            <select
              id="salary"
              v-model="form.salary"
              name="salary"
              class="border rounded w-full py-2 px-3"
              required
            >
              <option value="1 сая - 2 сая">1 - 2 сая</option>
              <option value="2 сая - 3 сая">2 - 3 сая</option>
              <option value="3 сая - 4 сая">3 - 4 сая</option>
              <option value="4 сая - 5 сая">4 - 5 сая</option>
              <option value="5 сая - 6 сая">5 - 6 сая</option>
              <option value="6 сая - 7 сая">6 - 7 сая</option>
              <option value="7 сая - 8 сая">7 - 8 сая</option>
              <option value="8 сая - 9 сая">8 - 9 сая</option>
              <option value="9 сая - 10 сая">9 - 10 сая</option>
              <option value="10 сая ба түүнээс дээш">
                10 сая ба түүнээс дээш
              </option>
            </select>
          </div>

          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2"> Байршил </label>
            <input
              type="text"
              v-model="form.location"
              id="location"
              name="location"
              class="border rounded w-full py-2 px-3 mb-2"
              placeholder="Компани байршил"
              required
            />
          </div>

          <h3 class="text-2xl mb-5">Компанийн мэдээлэл</h3>

          <div class="mb-4">
            <label for="company" class="block text-gray-700 font-bold mb-2"
              >Компанийн нэр</label
            >
            <input
              type="text"
              v-model="form.company.name"
              id="company"
              name="company"
              class="border rounded w-full py-2 px-3"
              placeholder="Компанийн нэр"
            />
          </div>

          <div class="mb-4">
            <label
              for="company_description"
              class="block text-gray-700 font-bold mb-2"
              >Компанийн тайлбар</label
            >
            <textarea
              id="company_description"
              v-model="form.company.description"
              name="company_description"
              class="border rounded w-full py-2 px-3"
              rows="4"
              placeholder="Танай компани юу хийдэг вэ?"
            ></textarea>
          </div>

          <div class="mb-4">
            <label
              for="contact_email"
              class="block text-gray-700 font-bold mb-2"
              >Холбогдох имэйл</label
            >
            <input
              type="email"
              v-model="form.company.contactEmail"
              id="contact_email"
              name="contact_email"
              class="border rounded w-full py-2 px-3"
              placeholder="Өргөдөл гаргагчидтай холбоо барих имэйл"
              required
            />
          </div>
          <div class="mb-4">
            <label
              for="contact_phone"
              class="block text-gray-700 font-bold mb-2"
              >Холбогдох утас</label
            >
            <input
              type="tel"
              v-model="form.company.contactPhone"
              id="contact_phone"
              name="contact_phone"
              class="border rounded w-full py-2 px-3"
              placeholder="Өргөдөл гаргагчидтай холбоо барих утас (заавал биш)"
            />
          </div>

          <div>
            <button
              class="bg-green-500 hover:bg-green-600 text-white font-bold py-2 px-4 rounded-full w-full focus:outline-none focus:shadow-outline"
              type="submit"
            >
              Ажлын байр нэмэх
            </button>
          </div>
        </form>
      </div>
    </div>
  </section>
</template>
